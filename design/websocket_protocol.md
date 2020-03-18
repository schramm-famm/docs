# Websocket Protocol

The server and the front-end clients must handle applying patches to a
conversation and users' carets in the conversation. The front-end clients
connect to the server via a WebSocket connection when a conversation is loaded.
Versioning is used by the server and clients to handle concurrency issues that
could arise when clients are out of sync. This document will outline the
protocol used to handle the WebSocket connections and the messages sent over the
connections.

## Messages
**5** types of messages can be sent over the WebSocket:
    * `Init`
    * `Update`
    * `Ack`
    * `UserJoin`
    * `UserLeave`

**Fields**:
* `type`: int
    * Indicates the type of the message. `Init` is 0, `Update` is 1, and so on.
* `data`: object
    * Payload of the message. Each type of message has a different format for
      the payload.

### `Init`
The initial message that is sent from the server to a client when the connection
to a conversation is established.

**Payload Fields**:
* `content`: string
    * Current conversation content.
* `version`: int
    * Current conversation version.
* `active_users`: object
    * Map of each active users' caret positions where the key is the user ID and
      the value is a map of the caret position.

**Format**:
```
{
    "type": 0,
    "data": {
        "content": "string",
        "version": int,
        "active_users": {
            "user-id": {
                "start": int,
                "end": int
            }
        }
    }
}
```

### `Update`
The messages sent from clients to the server to process and broadcast to other
clients. `Update` messages have the following subtypes:
* `Edit`
* `Cursor`

**Payload Fields**:
* `type`: int
    * Indicates the type of the `Update` message.
    * `0` is `Edit` and `1` is `Cursor`.
* `user_id`: int
    * ID of the user that sent the message.
* `version`: int
    * Conversation version that the user was on when the message was sent.
* `delta`: object
    * Map of integers representing the changes in the conversation state.
* `delta.caret_start`: int
    * Change in the user's start caret.
* `delta.caret_end`: int
    * Change in the user's end caret.

#### `Edit`
These messages represent a change in the conversation content, such as when a
user types or deletes letters.

**Additional Fields**:
* `patch`: string
    * Plaintext representation of a patch object generated using the
      [diff-match-patch](https://github.com/google/diff-match-patch) library.
* `delta.doc`: int
    * Change in the number of characters, not including HTML tags, in the
      document.

**Format**:
```
{
    "type": 1,
    "data": {
        "type: 0,
        "user_id": int,
        "version": int,
        "patch": "string",
        "delta": {
            "caret_start": int,
            "caret_end": int,
            "doc": int
        }
    }
}
```

#### `Cursor`
A `Cursor Update` message indicates that there was only a change in a user's
caret position. There are no additional fields.

### `Ack`
This message can be sent from clients and the server. An `Ack` is sent from a
client when it receives an `Edit Update` message to confirm the version that it
is currently on. When all clients, excluding the client that sent the original
message, have responded with an `Ack` for the version, the server broadcasts an
`Ack` to all clients, including the client that sent the original message, to
indicate that all clients have reached that version state.

**Payload Fields**:
* `version`: int
    * Conversation version that the sender is on.

### `UserJoin`
The message sent from the server to all active users in a conversation when a new
client joins the conversation.

**Payload Fields**:
* `user_id`: int
    * ID of the user.

### `UserLeave`
The message sent from the server to all active users in a conversation when a 
client leaves the conversation.

**Payload Fields**:
* `user_id`: int
    * ID of the user.

## Algorithm
This section will cover the algorithms that are implemented by the server and the
client to handle incoming messages.

### Caret Shifting
The server and clients keep track of all the active users' caret positions. The
following pseudocode describes how a caret is shifted when the conversation is
edited based on the caret position of the user that edited the conversation and
the `delta` object, which will have the `caret_start`, `caret_end`, and `doc`
fields.

```
if there was a selection range:
    range = [editor's start caret, editor's end caret]
else if there was an addition:
    range = [editor's start caret, editor's start caret + delta.caret_start]
else if there was a forward deletion:
    range = [editor's start caret, editor's start caret - delta.doc]
else if there was a normal deletion:
    range = [editor's start caret + delta.doc, editor's start caret]

if there was a normal addition:
    if editor's end caret < shifter's end caret:
        shifter's end caret += delta.doc
        if editor's end caret <= shifter's start caret:
            shifter's start caret += delta.doc
    return newly shifted caret

if range.end < shifter's end caret:
    shifter's end caret -= range.delta
    if range.end <= shifter's start caret:
        shifter's start caret -= range.delta
    else if range.start < shifter's start caret:
        shifter's start caret = range.start
else if range.end == shifter's end caret:
    shifter's start caret = range.end - range.delta
    shifter's end caret = range.end - range.delta
else if range.start < shifter's end caret:
    shifter's end caret = range.start
    if range.start < shifter's start caret:
        shifter's start caret = range.start

if there was a replacement with a positive delta.doc:
    do the same process ass the normal addition but with the editor's end caret
    equal to its start caret and delta.start instead of delta.doc
```

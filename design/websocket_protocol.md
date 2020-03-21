# Websocket Protocol

The server and the front-end clients must handle applying patches to a
conversation and users' carets in the conversation. The front-end clients
connect to the server via a WebSocket connection when a conversation is loaded.
Versioning is used by the server and clients to handle concurrency issues that
could arise when clients are out of sync. This document will outline the
protocol used to handle the WebSocket connections and the messages sent over the
connections.

## Table of Contents
* [Messages](#messages)
    * [`Init`](#init)
    * [`Update`](#update)
    * [`Ack`](#ack)
    * [`Sync`](#sync)
    * [`UserJoin`](#userjoin)
    * [`UserLeave`](#userleave)
* [Algorithms](#algorithms)
    * [Caret Shifting](#caret-shifting)
    * [Message Protocol](#message-protocol)

## Messages
The following types of messages can be sent over the WebSocket:
* [`Init`](#init)
* [`Update`](#update)
* [`Ack`](#ack)
* [`Sync`](#sync)
* [`UserJoin`](#userjoin)
* [`UserLeave`](#userleave)

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
This message is sent from the server to a client when the server receives an
`Edit Update` message from that client to confirm that the message has been
processed and broadcast.

**Payload Fields**:
* `version`: int
    * Version in the received `Edit Update` message.

### `Sync`
This message is sent from a client to the server when it receives an `Edit
Update` message to confirm the version that it is currently on. When all
clients, excluding the client that sent the original message, have responded
with an `Sync` for the version, the server broadcasts an `Sync` to all clients,
including the client that sent the original message, to indicate that all
clients have reached that version state.

**Payload Fields**:
* `version`: int
    * Version in the received `Edit Update` message.

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

## Algorithms
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
    do the same process as the normal addition but with the editor's end caret
    equal to its start caret and delta.start instead of delta.doc
```

### Message Protocol

#### Server
The server stores a checkpoint for each version of a conversation and removes a
version checkpoint when it receives a `Sync` message from all active users in
the conversation for the next version. The conversation version number is
incremented with every valid `Edit Update` message received from a client. The
checkpoint is used to handle `Cursor Update` messages from clients that are
behind on the conversation state. Each checkpoint will contain the following
fields:
* `version`: int
    * The conversation version number of this checkpoint.
* `active_users`: Object
    * User IDs are the keys and the value is another Object of the user's caret
      `start` and `end` at this conversation version.
* `sender_caret`: Object
    * Caret position (`start` and `end`) of the sender of the
      message that brought the conversation to this version.
* `delta`: Object
    * The deltas (`caret_start`, `caret_end`, and `doc`) that brought the
      conversation to this version.

The server will then follow the pseudocode below when processing `Update`,
`Ack`, and `Sync` messages.

```
receive msg
switch msg.type
    case edit update:
        apply msg.patch to conversation.content
        if patch failed:
            return
        conversation.version++
        if msg.version != conversation.version:
            msg.version = conversation.version
        broadcast message to all active clients, excluding the sender
        sender_caret = current sender caret position
        apply delta to caret of sender
        shift carets of all active clients
        store checkpoint object
    case cursor update:
        apply delta to caret of sender at msg.version checkpoint
        shift caret of sender at subsequent checkpoints based on the new caret
        position
        broadcast message to all active clients, excluding the sender
    case sync:
        remove user from list of awaiting syncs for the msg.version
        if all syncs for msg.version have been received:
            broadcast new sync msg to all active clients, including the sender
            remove checkpoint for msg.version - 1
```

#### Client
The client stores a version checkpoint when it receives an `Edit Update` message
and removes a version checkpoint when it receives a `Sync` message from the
server for the next version. The conversation version number is incremented with
every `Edit Update` message sent from the client and received from the server.
The checkpoint is used to handle `Cursor Update` messages from clients that are
behind on the conversation state. Each version checkpoint will contain the
following fields:
* `version`: int
    * The conversation version number of this checkpoint.
* `self_caret`: Object
    * Caret position (`start` and `end`) of the client and this conversation
      version.
* `active_users`: Object
    * User IDs are the keys and the value is another Object of the user's caret
      `start` and `end` at this conversation version.
* `sender_caret`: Object
    * Caret position (`start` and `end`) of the sender of the message that
      brought the conversation to this version.
* `delta`: Object
    * The deltas (`caret_start`, `caret_end`, and `doc`) that brought the
      conversation to this version.

A content checkpoint of the conversation is updated whenever a non-conflicting
`Edit Update` message is received. Non-conflicting means that the version number
of the message is `v + 1`, where v is the version number of the client. This
checkpoint represents the state of the server, so the client can handle
conflicting `Edit Update` messages in a similar way to the server. The
checkpoint will contain the following fields:
* `content`: string
    * The conversation content after the patch from the `Edit Update` message is
      applied to the previous checkpoint.

Every time the client sends an `Edit Update` message, it adds the `patch` and
`delta` of the message to a patch buffer. The patch buffer is dequeued when an
`Ack` message is received.

The following pseudocode describes what the client does when sending an `Edit
Update`.

```
patch = make patch with conversation.content as original state and conversation.innerHTML as new state
conversation.version++

caret = get client's current caret position
textSize = get number of characters in the conversation

delta.caret_start = caret.start - conversation.self_caret.start
delta.caret_end = caret.end - conversation.self_caret.end
delta.doc = textSize - conversation.textSize

send Edit Update message with conversation.version, patch, and delta
add patch and delta to patchBuffer

for user_id, caret in conversation.active_users:
    conversation.active_users[user_id] = shiftCaret(caret, conversation.self_caret, delta)

conversation.self_caret = caret
conversation.textSize = textSize
```

The following pseudocode blocks cover how the client handles `Cursor Update`,
`Edit Update`, `Ack`, and `Sync` messages.

**Cursor Update Handling:**
```
apply delta to caret of msg.sender at checkpoint.version[msg.version]
for (v = msg.version + 1; v < checkpoint.version.length; v++):
    receiver_caret = checkpoint.version[v - 1].active_users[msg.sender]
    sender_caret = checkpoint.version[v].sender_caret
    delta = checkpoint.version[v].delta
    checkpoint.version[v] = shiftCaret(receiver_caret, sender_caret, delta)
```

**Edit Update Handling:**
```
apply msg.patch to checkpoint.content
if patch failed:
    return

conversation.content = checkpoint.content
sender_caret = checkpoint.version[msg.version - 1].active_users[msg.sender]
self_caret = checkpoint.version[msg.version - 1].self_caret

checkpoint.version[msg.version].self_caret = shiftCaret(self_caret, sender_caret, msg.delta)
conversation.self_caret = checkpoint.version[msg.version].self_caret

for user_id, caret in checkpoint.version[msg.version - 1].active_users:
    if user_id == msg.sender:
        continue
    checkpoint.version[msg.version].active_users[user_id] = shiftCaret(caret, sender_caret, msg.delta)
    conversation.active_users[user_id] = checkpoint.version[msg.version].active_users[user_id]

checkpoint.version[msg.version].active_users[msg.sender] = delta applied to sender_caret

if msg.version <= conversation.version:
    for patch, delta in patchBuffer:
        apply patch to conversation.content
        if patch failed:
            remove patch from patchBuffer
            conversation.version--
            continue

        for user_id, caret in conversation.active_users:
            conversation.active_users[user_id] = shiftCaret(caret, conversation.self_caret, delta)

        apply delta to conversation.self_caret
else if msg.version > conversation.version + 1:
    return error

conversation.version++
send Sync message for msg.version to server
```

**Ack Handling:**
```
if patchBuffer.length <= 0:
    return error

patch, delta = patchBuffer.dequeue()
self_caret = checkpoint.version[msg.version - 1].self_caret
checkpoint.version[msg.version].self_caret = delta applied to self_caret

apply patch to checkpoint.content
for user_id, caret in checkpoint.version[msg.version - 1].active_users:
   checkpoint.version[msg.version].active_users[user_id] = shiftCaret(caret, self_caret, delta)
```

**Sync Handling:**
```
remove checkpoint.version[msg.version - 1]
```

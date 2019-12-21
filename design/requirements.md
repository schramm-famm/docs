# Accounts

Users shall be _required_ to register an account to use the application.

Users shall be able to register by _either_:
  * providing a unique **email**, a **name**, and a **password**
  * authenticating through their Google or Facebook account

Users shall have the _option_ to set a _single_ custom **avatar** for their
account.

Users shall have the _option_ to set up multi-factor authentication for their
account.

Users shall have the _option_ to set a custom **nickname** for themselves
_for each_ **conversation**.

# Conversations (metadata)

## Creating

Users shall be able to create _multiple_ **conversations**.

Users shall be able to create a **conversation** by providing a **name** for the
**conversation** and any amount of **users** to be invited to the
**conversation**. A **conversation** can be made up of _one or more_ **users**.

Users shall be able to specify **users** to invite to a conversation by entering
an **email**. This will send an **invitation** to the given user in the
application and through their **email**.

Users shall be _required_ to assign a _single_ **role** _for each_ **user** in
a new conversation. The allowed roles are:
  1. **OWNER**  
    a) automatically assigned to creator  
    b) one per **conversation**  
  2. **ADMIN**
  3. **USER**

Users shall have the _option_ to set a _single_ custom **picture** for a
new **conversation**.

Users shall have the _option_ to set a _single_ custom **description** for a
new **conversation**.

## Updating

Users shall be able to join a **conversation** by accepting an invitation for
that specific **conversation**.

Users shall be able to decline an invitation to a **conversation**.

**USER+** users in an existing conversation shall be able to invite other users
to the **conversation**, with the following conditions:
  * **OWNER** users can assign **ADMIN** or **USER** role to new **users**
  * **USER** & **ADMIN** users can assign **USER** role to new **users**

**USER+** users in an existing **conversation** shall be able to update the
**name**, **picture**, and **description** of the **conversation**.

**OWNER** users in an existing **conversation** shall be able to update the role
of any non-**OWNER** user.

Users in an existing **conversation** shall be to remove themself from the
**conversation**.

**ADMIN+** users in an existing **conversation** shall be able to remove any
**USER** user from the **conversation**.

**OWNER** users in an existing **conversation** shall be able to remove any
non-**OWNER** user from the **conversation**.

## Deleting
**OWNER** users in an existing **conversation** shall be able to delete the
**conversation**. This will require entering the **name** of the
**conversation** and the **password** of the **user**.

# Conversations (content)

Users shall be able to enter and delete text in a **conversation**.

Users shall be able to apply styling to text in a **conversation**. The
styling options are:
  * bold
  * italics
  * underline
  * background colour (highlight)
  * font family
  * font colour
  * font size

Users shall be able to format text in a **conversation** in the following
ways:
  * justification
  * lists (ordered or undordered)

(REVIEW) Users shall be able to insert images and gifs in a **conversation** which
will be anchored as characters.

Users shall be able to set text in a **conversation** as a hyperlink to a
web page.

Users shall be able to click on hyperlink text in a **conversation** to open
the linked web page in a new tab.

Users shall be able to type the **name** of another **user** in a
**conversation** with a prefixed "@" symbol to send that user a notification.

Users shall be able to lock text in a **conversation** so that it cannot be
modified.

Users shall be able to access a list of all the locked text in a
**conversation**.

(REVIEW) Users shall be able to unlock previously-locked text in a **conversation**
so that it can be modified, with the following conditions:
  * locked text can be unlocked by the **user** who originally locked it
  * locked text can be unlocked by any **user** with a greater **role** than
  the **user** who originally locked it

# History

Users shall be able to access a list of changes made to a **conversation**.

Users shall be able to filter the list of changes made to a **conversation**
based on:
  * start time
  * end time
  * user
  * keywords
  * type of change (addition/deletion/styling/formatting)

Users shall be able to see a specific pre-filtered list of changes made to a
**conversation** that shows only the changes made since they last had the
**conversation** open.

# Notifications

Users shall receive both a browser notification and an email when invited to a
**conversation**.

Users shall receive both a browser notification and an email when tagged in a
**conversation**.

Users shall receive a browser notification when another **user** modifies the
text in a **conversation** while the browser tab is not open.

Users shall receive a browser notification and an email when their **role** has
been changed in a **conversation**.

Users shall be able to _globally_ mute notifications _for all_
**conversations**. Global muting can be applied to just browser notifications or
just emails. Global muting can selectively be applied to the following
notification types:
  * invitation
  * text entered
  * text re-styled/re-formatted
  * user was tagged
  * user's role changed

Users shall be able to mute notifications _for each_ **conversation** for a set
amount of time. **Conversation**-specific muting can be applied to just browser
notifications or just emails. **Conversation**-specific muting can selectively
be applied to the following notification types:
  * text entered
  * text re-styled/re-formatted
  * user was tagged
  * user's role changed

Users shall receive a visual indication when another **user** modifies the text
in a **conversation** while the browser tab is open, but the conversation is not
open.

# Mini-map

Users shall be shown a **mini-map** when they have a **conversation** open.  The
**mini-map** will be a small section of the browser page that displays the
entire **conversation** in a smaller format than the **conversation** area
itself. The position of all active **users** will be displayed in the
**mini-map**.

Users shall be able to click on a **user's** position indicator in the
**mini-map**, which will adjust their main **conversation** view to the position
of the **user** they clicked on.

Users shall be shown real-time inidicators of other **users** typing in the
**conversation** next to the **users'** position indicators on the **mini-map**.

(REVIEW) Users shall be shown the position of the **tags** in a **conversation**
that refer to them on the **mini-map**.

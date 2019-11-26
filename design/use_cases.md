## Accounts
* email (unique)
* password
* ID (unique)
* nickname (per convo)
* avatar
* MFA
* Google/Facebook OAuth

## Conversations (metadata)
* create
  * name
  * users (by id or email) -> assign role (admin)
  * picture
  * description
* join
  * by invitation (email/in-app)
    * must accept/decline
  * anyone can add users
* leave
  * leave button
  * \>= admin can kick out users
* delete
  * only allow owner to delete
  * require owner to enter name to confirm
  * require re-entering password
* modify
  * any user in convo can change:
    * name
    * picture
    * description
  * only owner can modify roles

## Conversations (content)
* bold, italicize, underline, bg colour, font colour, font, font size
* justification, lists (ordered, unordered)
* images, gifs
* links
* user tags
  * user tag would go to user position
  * prompt user when they type @
* locking sections
  * will show up in a list of locked sections

## History
* shown as list that can be filtered
* base list shows all changes made to document
* "since you've been gone" show automatically when user returns to convo
* filters
  * time range
  * user
  * keywords
  * patch type (+/-, style)

## Notifications
* convo invites -> email & in-app
* tags -> email & in-app
* changes to convo
  * 1 per convo, but updates w/ user that made changes
  * tab shows # of convo changes
  * new user, personal role change
* mute
  * tag-only
  * no notifications at all
  * temporary

## Mini-map
* shows active user's positions in document
* click on user takes you to position
* typing indicator
* indicate user tags positions

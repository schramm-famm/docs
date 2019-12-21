December 21

Looking into TLS is a thing.

Lookinginto specific microservices:

DB schema is in sandbox issues, and now in docs/design/database_schema.md

now adding to design

For Users:
 * username and email are unique, the key of the table will be the UUID.
 * have to look into 2 factor authentication, look into what else we need to store
 * Removing username, just using name
 * _Karen's gonna have to confirm user's email._
 * we can only invite users by email.
 * Get email thing working
 
 
Look into which MongoDB and how we are going to store settings in a db. Using document in the db?


___ to ___ tables will have their own 'microservices' there will be api's to check if id's exist 

We now don't need the 'user_sessions' table. Last seen is in 'users_to_conversations'

Igor said 'do-do'

Milestone for deliverable functionality

Have milestones set up by th 27th of december

Riley -> Users
Igor -> Conversations
Honor -> Patches: looking into time series database
Thao -> Looking into TLS for Heimdall, looking into Preferences


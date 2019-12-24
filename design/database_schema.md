* Store files (conversations) in filesystem
* Store file paths in the `conversations` table

# Tables
* fk = foreign key
* unq = unique

`conversations `

 ID (str, unq) | File_Path (str) | Name (str) | Picture (str) | Description (str)
 --- | --- | --- | --- | ---
UUID | \<UUID\>.html | Family | conversation_135254.png | Chilling with pals

`patches`

ID (str, unq) | Timestamp (ts) | Patch (str)| Convo_ID (str, fk) | User_ID (str, fk) | Type (enum)
 --- | --- | --- | --- | --- | ---
UUID | 2019-10-01-20:00:00 | \<some patch\> | UUID | UUID | ENUM(formatting)

`users`

ID (str, unq) | Email (str, unq) | Name (str) | Salt (str) | Password (str) | Avatar (str)
--- | --- | --- | --- | --- | ---
UUID | johnny85@gmail.com | John Smith | asdf-wqer-wert | asmnwefkjsdf | avatars/johnny_smithy.png

`users_to_conversations`

User_ID (str, fk) | Convo_ID (str, fk) | Role (enum) | Nickname (str) | Pending (bool) | Last_Opened (ts)
--- | --- | --- | --- | --- | ---
UUID | UUID | ENUM(admin) | johnnybby | True | 2019-12-21-13:45:00

`preferences`

User_ID (str, fk) | Preferences (JSON?)
--- | ---
UUID | Something

* Store files (conversations) in filesystem
* Store file paths in the `conversations` table

# Tables
* fk = foreign key

`conversations `

 ID (str, unq) | File_Path (str) | Name (str) 
 --- | --- | ---
UUID | \<UUID\>.xml | Family

`patches`

ID (str, unq) | Timestamp (ts) | Patch (str)| Convo_ID (str, fk) | User_ID (str, fk)
 --- | --- | --- | --- | ---
UUID | 2019-10-01-20:00:00 | \<some patch\> | UUID | UUID

`users`

ID (str, unq) | Email (str, unq) | Name (str) | Salt (str) | Password (str) | Avatar (str)
--- | --- | --- | --- | --- | ---
UUID | johnny85@gmail.com | John Smith | asdf-wqer-wert | asmnwefkjsdf | avatars/johnny_smithy.png

`user_sessions`

ID (str, unq) | User_ID (str, fk) | Login_Time (ts) | Last_Seen (ts)
--- | --- | --- | ---
UUID | UUID | 2019-10-01-20:00:00 | 2019-10-01-23:30:00

`users_to_conversations`

User_ID (str, fk) | Convo_ID (str, fk) | Role (enum) | Nickname (str)
--- | --- | --- | ---
UUID | UUID | ENUM(admin) | johnnybby

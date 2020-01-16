* Store files (conversations) in filesystem
* Store file paths in the `conversations` table

# Tables
* fk = foreign key
* unq = unique

`conversations `

 ID (int, unq) | Name (str) | Description (str)
 --- | --- | --- 
1 | Family | Chilling with pals

`patches`

ID (int, unq) | Timestamp (ts) | Patch (str)| Convo_ID (str, fk) | User_ID (str, fk) | Type (enum)
 --- | --- | --- | --- | --- | ---
1 | 2019-10-01-20:00:00 | \<some patch\> | UUID | UUID | ENUM(formatting)

`users`

ID (int,str, unq) | Email (str, unq) | Name (str) | Salt (str) | Password (str) | Avatar (str)
--- | --- | --- | --- | --- | ---
1 | johnny85@gmail.com | John Smith | asdf-wqer-wert | asmnwefkjsdf | avatars/johnny_smithy.png

`users_to_conversations`

User_ID (int, fk) | Convo_ID (str, fk) | Role (enum) | Nickname (str) | Pending (bool) | Last_Opened (ts)
--- | --- | --- | --- | --- | ---
1 | UUID | ENUM(admin) | johnnybby | True | 2019-12-21-13:45:00

`preferences`

User_ID (int, fk) | Preferences (JSON?)
--- | ---
1 | Something
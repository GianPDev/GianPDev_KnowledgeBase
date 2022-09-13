---
tags: [sql, mysql, database, postgres, sqlite]
---

[[Database Commands]]

### Enums or not to Enums?
https://cetra3.github.io/blog/implementing-a-jobq-sqlx/
https://softwareengineering.stackexchange.com/questions/305148/why-would-you-store-an-enum-in-db
https://dzone.com/articles/when-you-should-and-should-not

If it has ANY possibility of growing, DO **NOT** use ENUM. Create a table instead
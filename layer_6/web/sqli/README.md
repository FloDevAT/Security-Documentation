# 🌐 SQL-Injection (SQLi)

```
 ________  ________  ___       ___     
|\   ____\|\   __  \|\  \     |\  \    
\ \  \___|\ \  \|\  \ \  \    \ \  \   
 \ \_____  \ \  \\\  \ \  \    \ \  \  
  \|____|\  \ \  \\\  \ \  \____\ \  \ 
    ____\_\  \ \_____  \ \_______\ \__\
   |\_________\|___| \__\|_______|\|__|
   \|_________|     \|__|           
```

## What is SQL?

`SQL` stands for `Structured Query Language` and is a standarized query language designed for accessing databases. There are several different dialects but the general SQL standard always stays the same. 

In order to explain SQL a bit better, I will demonstrate it in a little example. Imagine we have a database with a table `note` which looks like this:

| id | title         | content                                                    |   |
|----|---------------|------------------------------------------------------------|---|
| 1  | Shopping List | I need to buy milk, eggs and potatoes.                     |   |
| 2  | Homework      | There is a Security assignment about SQLi until next week! |   |
| 3  | Chores        | I might clean my room again...                             |   |


And now we want to access a specific row of this table. We could execute following query in order to get the note with the id `1`:

```sql
SELECT  *
FROM    note
WHERE   id = 1
```

And this would result in following row:

| id | title         | content                                                    |   |
|----|---------------|------------------------------------------------------------|---|
| 1  | Shopping List | I need to buy milk, eggs and potatoes.                     |   |

For the next steps in this documentation you will need basic SQL knowledge, so I recommend doing a quick course: https://www.w3schools.com/sql/


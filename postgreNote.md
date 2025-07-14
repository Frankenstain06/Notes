# <span style= "color:#00FF00">POSTGRESQL NOTE</span>
---
## <span style= "color:#00FF00">Command at Terminal sql shell</span>

- `\list` / `\l` -> This is used to check if there is a existing database.
- `\! cls` -> clear the screen
- `CREATE DATABASE` -> This command create a database for us.

🔥 <span style= "color:RED">**After creating database we need to verify it.**</span>

- `\c database-name` -> This help to connect with a specefic database among many database.
- `drop database database-name` -> This delete the database.
- `\d table-name` -> To view the table in the terminal.



## <span style= "color:#00FF00">PGAdmin Instruction</span>

- **SELECT datname FROM pg_database** -> Create Database

#### <span style= "color:YELLOW">**This is the code for creating a table**</span>

 ```sql
CREATE TABLE Student(
	name VARCHAR(30),
	id INT,
	city VARCHAR(15)
);
```
1. `CREATE TABLE` -> **This is the command for creating table.**
2. `Fahim` -> **This is the name of the table.**
3. `name` `id` `city` -> **This is coloum and coloum value of the table**
4. `VARCHAR`-> **It is the data type of the coloum**
5. `(30)` -> **This is the size of the varchar character**

#### <span style= "color:YELLOW">**This sets value into the table**</span>
``` sql
INSERT INTO Fahim(coloumn_name)
VALUES(coloum_value)
```
# Database notes

How to connect to a mysql database?

* `mysql -h 192.168.137.138 -u root --password=enterthepassword`
  * `192.168.137.138` is the host that is running the mysql service.
  * `root` is the username to connect is the database
  * `enterthepassword` is the password for it.

## Examples

* Step 1 : List all the available databases
  * show databases;
* Step 2 : go to one of the database
  * use Users;      \#where Users is the database name.
* Step 3 : We then need a list of tables in this database, and what all columns and rows are there in the each table. Note that now we are inside a database, and all the information seen will be w.r.t this database.
  * show tables;
  * select \* from table1;
    * table1 is one of the tables from the list of tables.




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
  * 
* * *  * * select table\_name from information\_schema.tables;


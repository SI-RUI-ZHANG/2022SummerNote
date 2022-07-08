---
created: 07-04-2022
e: ⭐
tags: CS/php, CS/sql
---

# Introduction to Relational Databases

## SQLite Command Line Tool

The SQLite command line gives you the ability to create and modify SQLite databases from your computer. Note that you can also do this through PHP (which we will do later in this tutorial) but we will begin by using the SQLite command line tool to set up a database and learn the commands that you will need to know to interact with it in an efficient manner.

To start, [download and unzip today's source code](https://cs.nyu.edu/courses/spring22/CSCI-UA.0061-001/sourcecode/19_SQLite.zip) and place into your MAMP folder. Next, open up a command line interface on your local computer (Mac: search for and launch the "Terminal" program; Windows: search for and launch the "command prompt" program). Next, navigate to your MAMP folder in your command line interface. If your MAMP folder is stored in your "Documents" folder, then you should be able to access it by issuing the following commands:

```bash
cd Documents
cd MAMP
cd 19_SQLite
cd databases
```

List all of the files in this directory (`ls` on a Mac, `dir` on a PC) - you should see a number of files, including that begin with 'sqlite3' (one called 'sqlite3' (for Mac) and one called 'sqlite3.exe' (for PC)). This is the 'SQLite command line tool' which can be used to edit and manipulate SQLite databases. Execute the program appropriate for your operating system by typing its full name (`sqlite3` on a Mac, `sqlite3.exe` on a PC) and hit Enter. Output like the following will appear:

This is the SQLite command line interface that we will be using to create our database which will (eventually) be used on the web. Before we go any further let's create a new database. Type the following command and hit enter:

```shell
.open to_do_list.db
```

The `.open` command will try and open a database called "to_do_list.db" in the current folder. Because no such database exists this will create a new database with this name.

### Tables

A _database_ is defined as a "structured set of data". Databases achieve this structure through the use of _tables_. Tables are designed to hold specific _fields_ of different data types -- for example, if we wanted to store information for a to-do list application we could set up a table that looks like the following:

| Table Name: items |         |
| ----------------- | ------- |
| id                | INTEGER |
| title             | TEXT    |
| status            | TEXT    |

The table above describes what type of data will be stored in the table. To actually store data in the table we create a _record_. For example, in the table above we might store a record that looks like the following:

```bash
id: 1
title: walk the dog
status: in progress
```

As you can see, our record uses the same fields as the "items" table. The table is the organizational structure that defines what kind of data is being stored, and the record is the actual implementation of that structure using actual data.

It's important to note that tables can contain any number of records, and each record must match the organizational structure of the table. For example, here are some additional records we could add to our table:

```bash
id: 2
title: take out the trash
status: in progress

id: 3
title: finish micro assignment
status: completed

id: 4
title: study for web dev final
status: in progress
```

Databases can hold multiple tables (you aren't limited to just one) and tables can hold multiple records.

### Creating tables

You can create a new table by writing a command in the "SQL" language. SQL stands for "Structured Query Language" is is designed to be a universal language that is supported by all relational database management engines.

The syntax for creating a new table using SQL is as follows:

```sql
CREATE TABLE table_name (column_name1 data_type1, column_name2 
    data_type2, ..... , column_nameN data_typeN);
```

Note: SQL is a **case-insensitive** language, so writing "CREATE TABLE" in all uppercase is note required.

SQLite supports a few different data types. Data stored in a table should conform to these data types, otherwise the record may be rejected. The SQLite data types include:

- TEXT: a string
- INTEGER: a signed (positive or negative) integer
- REAL: a signed floating point number
- NUMERIC: an integer or a floating point value

Tables should have one column (and only one column) that is used to uniquely identify a record. In the example above the "id" column uniquely identifies each record as each record stores a unique integer which serves as its identifier. We refer to this unique column as a "_primary key_". Tables should be set up with a primary key when they are created, and you can also have the database automatically assign a value to this primary key when the data is added to the table.

Here's the SQL needed to create the "items" table that we described above:

```sql
CREATE TABLE items (id INTEGER PRIMARY KEY AUTOINCREMENT, title TEXT, status TEXT);
```

Type this command into the SQLite command line interface and hit enter to create the table.

This says "Create a new table called items. It has 3 columns - 'id' (an integer, the primary key of the table, it should automatically set itself with a unique integer every time data is inserted), 'title' (a string of text), 'status' (a string of text)"

You only have to create a table once. Once it's created you can add, remove, update and retrieve data from the table.

Let's create a second table for our database which will store the names of some Pokemon (this is just for demo purposes and we will remove this table later). Execute the following SQL statement:

```sql
CREATE TABLE pokemon (id INTEGER PRIMARY KEY AUTOINCREMENT, name TEXT, hit_points INTEGER);
```

### Show List of Existing Tables

You can ask SQLite to show you the names of all tables in your database by issuing this command:

```sql
.tables
```

If you would like to see the organizational structure of a table you can issue this command (replace 'table_name' with the name of the table you are concerned with):

```sql
.schema table_name
```

### Deleting Tables

You can remove a table from the database using the following command. Note that this will delete all records in the table as well, so make sure you really don't need this table before you do this! Since we really don't need the 'pokemon' table we can safely remove it from our database:

```sql
DROP TABLE pokemon;
```

## Working with Records

Tables serve as the foundation of your database. Next we need to learn how to add, remove, update and retrieve records from our tables.

### Inserting Data

You can insert data into a table using the following syntax:

```sql
INSERT INTO table_name (column_name1, column_name2, ... , column_nameN) VALUES (value1, value2, .... , valueN);
```

Let's insert a few records into the `items` table to store a few "to-do list" items for our application:

```sql
INSERT INTO items (title, status) VALUES ('walk the dog', 'in progress');
INSERT INTO items (title, status) VALUES ('finish micro assignment', 'completed');
INSERT INTO items (title, status) VALUES ('study for web dev final', 'in progress');
```

Note how we didn't have to insert anything into the `id` column since this column will automatically insert a unique integer into the table upon insertion of a new record.

Also note that strings must be delimited with single quotation marks.

### Viewing / Retrieving Data

You can view all records in a table by running the following SQL statement:

```sql
SELECT * FROM table_name;
```

The **`*`** character in this example is a "wildcard" that says "retrieve all columns" - if you want to limit the columns you retrieve you could list them out like this:

```sql
SELECT id, title, status FROM items;
```

Let's try retrieving all data from our sample table using this SQL:

```sql
SELECT * FROM items;
```

You should see the following appear:

```shell
1|walk the dog|in progress
2|finish micro assignment|completed
3|study for web dev final|in progress
```

Now let's limit the result to just the 'title' and 'status' columns:

```sql
SELECT title, status FROM items;
```

You will see that our output has been adjusted and doesn't include the `id` column:

```shell
walk the dog|in progress
finish micro assignment|completed
study for web dev final|in progress
```

`SELECT` queries are very powerful and we are only covering the basics of what they can do here. One very useful thing we can add to a `SELECT` query is the ability to limit data based on certain conditions. We can do this using the `WHERE` clause, like this:

```sql
SELECT * FROM table_name WHERE column_name1 [=/</>] desired_value1 [=/</>] column_name2 = desired_value2 ... [=/</>] column_nameN = desired_valueN;
```

Conditions can be enumerated as Boolean expressions connected with logical operators. Note that SQL uses '=' for comparison as well as assignment.

For example, to obtain just the "in progress" records from the table we could execute the following query:

```sql
SELECT * FROM items WHERE status = 'in progress';
```

In addition, we can ask SQLite to retrieve items from the database in a particular order. The syntax for this query is:

```sql
SELECT * FROM table_name ORDER BY column_name [ASC/DESC]
```

`ASC` stands for "ascending" and `DESC` stands for "descending". For example:

```sql
SELECT * FROM items ORDER BY title ASC;
```

This will result in the records being sorted in ascending order based on the contents of the 'title' column, like this:

```shell
2|finish micro assignment|completed
3|study for web dev final|in progress
1|walk the dog|in progress
```

### Deleting Data

You can delete records from a table by executing a DELETE query:

```sql
DELETE FROM table_name WHERE conditions;
```

Let's delete all records that are "completed" from the table using this SQL:

```sql
DELETE FROM items WHERE status = 'completed';
```

Next, retrieve all data from the table to see the changes to the records:

```sql
SELECT * FROM items;
```

You'll notice that the one completed item is now missing from the table:

```sql
1|walk the dog|in progress
3|study for web dev final|in progress
```

### Updating Data

Existing records can be updated using a `UPDATE` query:

```sql
UPDATE table_name SET column_name1 = value1, column_name2 = value2, ..., column_nameN = valueN WHERE conditions;
```

For example, to set record #1 ('walk the dog') to completed you could execute the following query:

```sql
UPDATE items SET status = 'completed' WHERE id = 3;
```

## Using SQLite with PHP

The PHP language has a built-in library that allows you to connect to and work with a SQLite database through your programs. This section of the tutorial will walk you through the basics of setting up this connection and executing queries against your databases.

### File Organization

Your database files (.db) contain ALL of the stored data for your application. It's important make sure that these files are not stored in your `public_html` folder -- if they are it is very possible a user can get a link to your database and download all of your site data with one click! For a basic application this may not be much of an issue, but imagine if you are storing sensitive information such as names, addresses, phone numbers or even usernames / passwords in a database!

To get around this you should set up a separate folder called 'databases' outside of your application code folder to store your databases. You can then have PHP access your database using the absolute file path. For the 'To Do List' application that we're building here the file organization should look as follows:

```shell
19_SQLite/
          databases/    (folder where your database is stored)
          to_do_list/   (folder where your application code is stored)
```

When you deploy your application to a public web server you will need to adjust your file path so that your "live" application points to the correct location of your database.

### Connection Object

The first thing you will need to do in your PHP script is to connect to your database. You can do this by establishing a 'connection object' using the following code:

```shell
// step 1: we need to identify the full file path of where our
// databases are stored on the server.
$path = '/your/file/path/goes/here';

// step 2: connect to our database, making sure to use the full
// file path when specifying the database file location
$db = new SQLite3($path.'/to_do_list.db');
```

Because you will most likely be connecting to your database through multiple PHP files it would be helpful to store the file path inside of a separate file that you can edit to update your entire site (just like updating an external CSS document can update the styles across your whole site). You can create a separate PHP file (called `config.php`) and simply include it in your code like this:

#### config.php

```php
<?php $path = '/your/file/path/goes/here'; ?>
```

#### some_php_document.php

```php
<?php 
// step 1: import the file path variable ($path)
include('config.php');

// step 2: connect to our database, making sure to use the full
// file path when specifying the database file location
$db = new SQLite3($path.'/to_do_list.db');
?>
```

### Running a Query (basic)

The basic process for running a query through PHP is as follows:

- Create a connection to the database
- Construct the query using a string
- Execute the query using the connection object
- Deal with any return values (for example, when selecting data you will receive an array of records that matched your query)

### Running an INSERT Query

To insert data into your database you can run an INSERT query using the following syntax:

```php
<?php $path = '/your/file/path/goes/here'; ?>
```

#### some_php_document.php

```php
<?php 
// step 1: import the file path variable ($path)
include('config.php');
// step 2: connect to our database, making sure to use the full
// file path when specifying the database file location
$db = new SQLite3($path.'/to_do_list.db');
// step 3: construct an INSERT query
$sql = "INSERT INTO items (title, status) VALUES ('feed the cat', 'in progress')";
// step 4: run the query
$result = $db->query($sql);
// done!
?>
```

Note that you are not limited to adding in hard-coded strings -- you can replace 'feed the cat' with a variable if you want. However, when working with variables you should prepare your strings so that single quotation marks within the string don't interfere with the string delimiters. The easiest way to do this is to use the SQLite built-in `escapeString` method, like this:

```php
$original_title = 'feed the cat';
$clean_title = $db->escapeString($original_title);
```

After you run an INSERT query the database can provide you with some additional information if you need it. For example, in this query we are inserting into a table that has an auto-increment field for the 'id' - if you want to obtain the integer that goes along with the record you just inserted you can run this code after the query executes:

```php
$id = $db->lastInsertRowID();
```

In addition, you can also get a count of how many records were affected by your last query by running this code after the query executes:

```php
$rows_affected = $db->changes();
```

### Running a DELETE or UPDATE Query

UPDATE and DELETE queries work similarly to INSERT queries:

```php
<?php 

// step 1: import the file path variable ($path)
include('config.php');

// step 2: connect to our database, making sure to use the full
// file path when specifying the database file location
$db = new SQLite3($path.'/to_do_list.db');

// step 3: construct a DELETE query
$sql1 = "DELETE FROM items WHERE title = 'feed the cat'";

// step 4: run the query
$result = $db->query($sql1);

// set up another query
$sql2 = "UPDATE items SET status = 'completed WHERE title = 'study for web dev final'";

// run the second query
$result = $db->query($sql2);

// done!
?>
```

Using the `$db->changes()` function can be very useful for these kinds of queries since this will act as a confirmation that the record was deleted / updated.

### Running a SELECT Query

A SELECT query will return data to your PHP program -- in order to handle this data you will need to write a bit of extra code to process this data. The following example shows how to obtain all data from our `items` table:

```php
<?php 

// step 1: import the file path variable ($path)
include('config.php');

// step 2: connect to our database, making sure to use the full
// file path when specifying the database file location
$db = new SQLite3($path.'/to_do_list.db');

// step 3: construct a SELECT query
$sql1 = "SELECT (id, title, status) FROM items";

// step 4: run the query
$result = $db->query($sql1);

// step 5: iterate over the results
while ($row = $result->fetchArray()) {
    // extract the relevant info from the query into some variables
    $id = $row[0];
    $title = $row[1];
    $status = $row[2];

    print "$id - $title - $status";
}

// done!
?>
```

## Deploying a Database Enabled Application to i6

- Open a SFTP connection to the i6 server
- Create a folder under your HOME directory called `databases` - **FOR SECURITY PURPOSES THIS FOLDER SHOULD NOT BE INSIDE OF YOUR `public_html` FOLDER!** - your directory structure on the server will now look like this:

```shell
    /home/NET_ID               (your home directory)
                /databases     (your database directory)
                /public_html   (a link to your public_html directory)
```

- Set the permissions on the `databases` folder to be fully accessible to all users on the server (777)
- Upload your database file (.db) to this folder - also update the permissions on your database file so that it also has full permissions (777)
- Copy the absolute file path to this directory (`/home/NET_ID/databases`)
- Upload your application code to your `public_html` folder
- Edit your application code so that it points to the absolute URL to your database folder on the server

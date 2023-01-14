In MySQL, there are several types of keys that can be used to enforce constraints and improve the performance of the database. Here's a table summarizing the different types of keys and their characteristics:

| Key Type | Description | Unique | Not Null | Stable |
| --- | --- | --- | --- | --- |
| Primary Key | A unique identifier for each row in a table. Used to enforce the integrity of the data and to establish relationships between tables. | Yes | Yes | Yes |
| Foreign Key | A column or set of columns in a table that references the primary key of another table. It is used to establish a link or relationship between the data in the two tables. | No | Yes | Yes |
| Unique Key | A column or set of columns that enforce the uniqueness of the values in the table. Similar to a primary key, but it allows for null values. | Yes | No | Yes |
| Index | A database object that is used to speed up the retrieval of data from a table. Can be created on one or more columns in a table and improves the performance of SELECT statements. | No | No | No |

Please note that, a table can have multiple keys of different types, but only one primary key.




# Primary key
In a MySQL database, a primary key is a unique identifier for each row in a table. It is used to enforce the integrity of the data and to establish relationships between tables. A primary key is a column or set of columns that have the following characteristics:

-   Unique: Each value in the primary key column or set of columns must be unique across all rows in the table.
-   Not Null: The primary key column or columns cannot contain null values.
-   Stable: The primary key value cannot be changed after the row is inserted.

Here's an example of a table called "customers" with a primary key:

| customer\_id | name | email |
| --- | --- | --- |
| 1 | John | [john@example.com](mailto:john@example.com) |
| 2 | Sarah | [sarah@example.com](mailto:sarah@example.com) |
| 3 | Michael | [michael@example.com](mailto:michael@example.com) |

In this example, "customer\_id" is the primary key for the table. It is unique for each customer and cannot be null or changed once it's set.

Other than primary key, MySQL supports other keys as well which are:

-   Foreign key: A foreign key is a column or set of columns that references a primary key in another table. It is used to establish a link between the data in two tables.
-   Unique key: A unique key is a column or set of columns that enforce the uniqueness of the values in the table. It is similar to a primary key, but it allows for null values.
-   Index: An index is a database object that is used to speed up the retrieval of data from a table. It can be created on one or more columns in a table and it improves the performance of SELECT statements.

Here's an example of a table called "orders" with a foreign key and unique key:

| order\_id | customer\_id | product | order\_date |
| --- | --- | --- | --- |
| 1 | 2 | Pen | 2021-01-01 |
| 2 | 1 | Book | 2021-01-02 |
| 3 | 3 | Pencil | 2021-01-03 |

In this example, "customer\_id" is a foreign key, it references the primary key of the "customers" table. "order\_id" is a unique key and it ensures that the order\_id is unique across the table.

Please note that, it is not necessary that every table must have a primary key, but it is good practice to have one and it is also necessary for the foreign key.


# Foreign keys
A foreign key is a column or set of columns in a table that references the primary key of another table. It is used to establish a link or relationship between the data in the two tables. This relationship is known as referential integrity and it helps to maintain the consistency and accuracy of the data in the database.

For example, consider two tables: "customers" and "orders". The "customers" table has a primary key "customer\_id" and the "orders" table has a foreign key "customer\_id" that references the primary key "customer\_id" in the "customers" table.

The "customers" table might look like this:

| customer\_id | name | email |
| --- | --- | --- |
| 1 | John | [john@example.com](mailto:john@example.com) |
| 2 | Sarah | [sarah@example.com](mailto:sarah@example.com) |
| 3 | Michael | [michael@example.com](mailto:michael@example.com) |

And the "orders" table might look like this:

| order\_id | customer\_id | product | order\_date |
| --- | --- | --- | --- |
| 1 | 2 | Pen | 2021-01-01 |
| 2 | 1 | Book | 2021-01-02 |
| 3 | 3 | Pencil | 2021-01-03 |

The "customer\_id" column in the "orders" table is a foreign key that references the primary key "customer\_id" in the "customers" table. This creates a one-to-many relationship between customers and orders: one customer can have many orders, but each order is associated with only one customer.

Foreign keys can also be used to create many-to-many relationships. For example, consider two tables "books" and "authors". A book can have multiple authors and an author can write multiple books, so we can create a table "book\_authors" that has two foreign keys "book\_id" and "author\_id" referencing the primary keys in "books" and "authors" tables respectively. This creates a many-to-many relationship between books and authors.
Sure, here's an example of how the "books" and "authors" tables might look like and a third table "book\_authors" to create a many-to-many relationship between them:

The "books" table:

| book\_id | title | ISBN |
| --- | --- | --- |
| 1 | The Great Gatsby | 1234567890 |
| 2 | To Kill a Mockingbird | 0987654321 |
| 3 | Pride and Prejudice | 1029384756 |

The "authors" table:

| author\_id | name |
| --- | --- |
| 1 | F. Scott Fitzgerald |
| 2 | Harper Lee |
| 3 | Jane Austen |

The "book\_authors" table:

| book\_id | author\_id |
| --- | --- |
| 1 | 1 |
| 1 | 2 |
| 2 | 2 |
| 3 | 3 |

In this example, the "book\_id" and "author\_id" columns in the "book\_authors" table are foreign keys that reference the primary keys "book\_id" and "author\_id" in the "books" and "authors" tables respectively. This creates a many-to-many relationship between books and authors: one book can have multiple authors, and one author can write multiple books.

In this case, the "book\_authors" table is called as join table, it is used to join the many-to-many relationship between books and authors.

It is also possible to add additional fields to the join table like, for example, the role of the author in the book or the date of association, which would be specific to the relationship between the books and authors table.

Foreign keys can also enforce referential integrity constraints such as ON DELETE CASCADE and ON UPDATE CASCADE. These constraints specify what should happen when a primary key value is deleted or updated. For example, if ON DELETE CASCADE is specified, when a customer is deleted from the "customers" table, all the corresponding orders in the "orders" table will also be deleted.
Sure, here's an example of how to create a many-to-many relationship between two tables "books" and "authors" using a join table "book\_authors" and foreign keys:

1.  Creating the "books" table:

```sql
CREATE TABLE books (
    book_id INT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    ISBN VARCHAR(255) NOT NULL
);

```

2.  Creating the "authors" table:

```sql
CREATE TABLE authors (
    author_id INT PRIMARY KEY,
    name VARCHAR(255) NOT NULL
);

```

3.  Creating the "book\_authors" join table with foreign keys:

```sql
CREATE TABLE book_authors (
    book_id INT,
    author_id INT,
    PRIMARY KEY (book_id, author_id),
    FOREIGN KEY (book_id) REFERENCES books(book_id) ON DELETE CASCADE,
    FOREIGN KEY (author_id) REFERENCES authors(author_id) ON DELETE CASCADE
);

```

In this example, we are creating a join table called "book\_authors" with two foreign keys "book\_id" and "author\_id" that reference the primary keys in the "books" and "authors" tables respectively. This creates a many-to-many relationship between books and authors: one book can have multiple authors, and one author can write multiple books.

The ON DELETE CASCADE is a referential action that is used to specify what should happen when a primary key value is deleted. For example, if ON DELETE CASCADE is specified, when a book is deleted from the "books" table, all the corresponding authors in the "book\_authors" table will also be deleted.

Foreign keys are extremely powerful tools that allow you to create relationships between tables and ensure the consistency and accuracy of your data.

# Uniqe keys

A unique key is a column or set of columns in a table that enforces the uniqueness of the values in the table. It is similar to a primary key, but it allows for null values. A table can have multiple unique keys, but each unique key must have a unique set of values across the table.

For example, consider a table called "employees". An employee can have a unique employee ID, but they can also have a unique email address. In this case, you can have two unique keys in the table: one for the "employee\_id" column and one for the "email" column.

Here's an example of a table called "employees" with two unique keys:

| employee\_id | name | email | phone |
| --- | --- | --- | --- |
| 1 | John | [john@example.com](mailto:john@example.com) | 9876 |
| 2 | Sarah | [sarah@example.com](mailto:sarah@example.com) | 1234 |
| 3 | Michael | [michael@example.com](mailto:michael@example.com) | 4321 |

In this example, "employee\_id" and "email" both are unique keys. Both of them have unique values across the table, it ensures that there are no duplicate employee ID or email addresses in the table.

You can also create unique keys on multiple columns. For example, you can create a unique key on the combination of two columns such as "name" and "email" to make sure that no two employees have the same name and email address.

One of the advantages of using unique keys is that it allows for more flexibility in the data model. You can create multiple unique keys for different columns or combinations of columns, which means that you can have multiple ways of identifying a row in a table. Another advantage is that unique keys can improve the performance of SELECT statements.

You can create a unique key in MySQL using the "UNIQUE" keyword in the CREATE TABLE statement, or you can add it later using the ALTER TABLE statement. Also, you can use the "SHOW INDEX" command to check which unique keys exist on a table.

Certainly, here are some examples of how to create and use unique keys in MySQL:

1.  Creating a unique key in a new table:

```sql
CREATE TABLE employees (
    employee_id INT NOT NULL,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    phone VARCHAR(255) NOT NULL,
    UNIQUE (email),
    PRIMARY KEY (employee_id)
);

```

In this example, we are creating a new table called "employees" with three columns: "employee\_id", "name" and "email". The "UNIQUE" keyword is used to create a unique key on the "email" column.

2.  Creating a unique key on multiple columns:

```sql

ALTER TABLE employees ADD UNIQUE (name, email);

```

In this example, we are adding a unique key on the combination of the "name" and "email" columns in the "employees" table.

3.  Creating a unique key after table is created:

```sql
ALTER TABLE employees ADD UNIQUE (phone);

```

This code will add unique key on phone column after table is created.

4.  Dropping a unique key:

```sql
ALTER TABLE employees DROP INDEX email_unique;

```

In this example, we are dropping the unique key named "email\_unique" from the "employees" table.

5.  Checking for existing unique keys:

```sql
SHOW INDEX FROM employees;

```

This command will show all the indexes and keys on the "employees" table, including any unique keys.

# index 
An index is a database object that is used to speed up the retrieval of data from a table. It can be created on one or more columns in a table and it improves the performance of SELECT statements. An index is similar to an index in a book, it provides a quick way to look up a specific value or range of values in a table.

For example, consider a table called "employees" with millions of rows. Without an index, if you want to find all employees with the last name "Smith", the database would have to scan through every row of the table, which could take a long time. However, if there is an index on the "last\_name" column, the database can quickly look up all the rows with the value "Smith" in the index, and retrieve the corresponding data from the table.

Here's an example of how to create an index on a table called "employees":

```sql
CREATE INDEX last_name_index ON employees (last_name);

```

In this example, we are creating an index called "last\_name\_index" on the "last\_name" column of the "employees" table. Now, when you run a query that looks up the last name "Smith", the database can use this index to quickly find all the matching rows.

You can also create an index on multiple columns:

```sql
CREATE INDEX name_index ON employees (last_name, first_name);

```

Also, you can create unique index on multiple columns:

```sql
CREATE UNIQUE INDEX email_index ON employees (email);

```

You can also drop an index if you no longer need it:

```sql
DROP INDEX last_name_index ON employees;

```

You can also check existing indexes on a table:

```sql
SHOW INDEX FROM employees;

```

This command will show all the indexes and keys on the "employees" table.


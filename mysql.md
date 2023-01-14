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

Foreign keys are extremely powerful tools that allow you to create relationships between tables and ensure the consistency and accuracy of your data.



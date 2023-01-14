#Mongodb

MongoDB is a popular, open-source, document-oriented NoSQL database. It is designed to handle large amounts of unstructured data and allows for easy scalability and high performance.

MongoDB stores data in a format called BSON (binary JSON), which is a binary-encoded serialization of JSON-like documents. This means that MongoDB stores data in a format that is similar to JSON, but with additional data types and a more compact binary representation.

MongoDB allows for flexible and dynamic schema design, as it does not enforce a strict schema like traditional relational databases. This means that documents in a collection can have different fields, and fields can be added or removed without having to alter the entire collection.

MongoDB also offers built-in support for sharding, which is a method of distributing data across multiple servers to improve performance and scalability.

MongoDB's rich query language and support for secondary indexes and full-text search makes it a popular choice for web and mobile applications, real-time analytics, content management, and other use cases that require high performance and scalability.

Please note that, MongoDB is not a replacement for all use-cases, it's best for use-cases that require handling big unstructured data, real-time analytics and high scalability.

Sure, here's a table with some common MongoDB syntax and examples to help you learn more quickly:

| Syntax | Description | Example |
| --- | --- | --- |
| `db.createCollection(<name>)` | Creates a new collection in the current database | `db.createCollection("students")` |
| `db.collection.insert(<document>)` | Inserts one or more documents into a collection | `db.students.insert({ name: "John", age: 25 })` |
| `db.collection.find(<query>)` | Queries a collection for documents matching a certain criteria | `db.students.find({ age: { $gt: 20 } })` |
| `db.collection.update(<query>, <update>)` | Updates one or more documents in a collection | `db.students.update({ name: "John" }, { $set: { age: 30 } })` |
| `db.collection.remove(<query>)` | Removes one or more documents from a collection | `db.students.remove({ age: { $lt: 25 } })` |
| `db.collection.aggregate(<pipeline>)` | Groups and transforms documents in a collection using an aggregation pipeline | `db.students.aggregate([{ $group: { _id: "$age", count: { $sum: 1 } } }])` |
| `db.collection.createIndex(<keys>)` | Creates an index on one or more keys in a collection | `db.students.createIndex({ name: 1` |

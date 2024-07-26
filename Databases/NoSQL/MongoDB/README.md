# MongoDB Guide

MongoDB is a NoSQL database management system that uses a flexible, document-oriented data model. It stores data in JSON-like BSON (Binary JSON) documents, making it suitable for applications with diverse data structures. MongoDB is particularly useful for handling large amounts of unstructured data and is often used in content management systems, real-time analytics, and applications with rapidly changing data. Here’s an overview of MongoDB's key concepts and components:

### MongoDB's data model components
MongoDB uses a flexible document data model, which consists of the following components:

1. **Documents**: Documents are the fundamental entities in MongoDB, akin to rows in a relational database. Each document is a set of key-value pairs, where values can be various data types, including other documents, arrays, and more.

    Example:
    ```json
    {
      "name": "Alice",
      "age": 30,
      "email": "alice@example.com",
      "created_at": {"$date": "2024-07-26T10:30:00Z"},
    }
    ```
    In this example, a document with fields `name`, `age`, `email` and `created_at` is defined.

    - BSON (binary JSON) is an extension of JSON designed to be efficient in both space and speed. BSON includes data types not present in JSON (like Date and binary data) and is optimized for fast encoding/decoding, making it more suitable for database storage and retrieval operations.

2. **Collections**: Collections are groups of documents and are analogous to tables in a relational database. A collection can hold multiple documents, and documents within a collection can have different structures, meaning it does not enforce a schema.

    Example:
    ```javascript
    db.users.insertOne({
      "name": "Alice",
      "age": 30,
      "email": "alice@example.com"
    })
    ```
    This example inserts a document into the `users` collection.

3. **Database**: A MongoDB database holds a set of collections. A single MongoDB server can have multiple databases, each providing physical separation of data.



### Data modeling
Designing a data model in MongoDB involves understanding how data will be accessed and using schema design patterns that optimize performance and flexibility.

**Example:**
Embedding vs. referencing:
- **Embedding**: Store related data within the same document. It is suitable for closely related data that is frequently accessed together.
  ```json
  {
    "name": "Alice",
    "contacts": [
      { "type": "email", "value": "alice@example.com" },
      { "type": "phone", "value": "123-456-7890" }
    ]
  }
  ```
- **Referencing**: Store related data in separate documents and reference them. It is suitable for large, independent, or less frequently accessed related data.
  ```javascript
  db.users.insertOne({ "name": "Alice" })
  db.contacts.insertOne({ "userId": ObjectId("..."), "type": "email", "value": "alice@example.com" })
  ```
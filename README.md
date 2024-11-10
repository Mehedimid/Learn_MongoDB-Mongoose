
# MongoDB and Mongoose Guide

This guide covers MongoDB and Mongoose methods, query operators, aggregation, filtering, and projection. 
Differences between MongoDB and Mongoose are highlighted where applicable.

---

## Table of Contents
1. [Basic CRUD Operations](#basic-crud-operations)
2. [Query Operators](#query-operators)
3. [Aggregation Framework](#aggregation-framework)
4. [Filtering and Projection](#filtering-and-projection)
5. [Mongoose-Specific Features](#mongoose-specific-features)

---

### 1. Basic CRUD Operations

#### MongoDB

- **`find()`**: Returns a cursor to all matching documents.
  ```javascript
  db.collection.find({ age: { $gt: 18 } });
  ```

- **`findOne()`**: Returns the first matching document.
  ```javascript
  db.collection.findOne({ name: "John" });
  ```

#### Mongoose

- **`find()`**: Returns an array of documents as a Promise, allowing chaining.
  ```javascript
  User.find({ age: { $gt: 18 } }).then(users => console.log(users));
  ```

- **`findOne()`**: Returns a single document as a Promise.
  ```javascript
  User.findOne({ name: "John" }).then(user => console.log(user));
  ```

> **Note**: In MongoDB, `find()` returns a cursor, while in Mongoose, `find()` returns a Promise.

---

### 2. Query Operators

#### Common Operators

- **Comparison**: `$eq`, `$ne`, `$gt`, `$gte`, `$lt`, `$lte`, `$in`, `$nin`
- **Logical**: `$and`, `$or`, `$not`, `$nor`
- **Element**: `$exists`, `$type`

#### Usage

- **MongoDB**:
  ```javascript
  db.collection.find({ age: { $gt: 18 } });
  ```

- **Mongoose**:
  ```javascript
  User.find({ age: { $gt: 18 } });
  ```

> **Note**: Query operators work the same way in both MongoDB and Mongoose.

---

### 3. Aggregation Framework

- **$match**: Filters documents based on conditions.
- **$group**: Groups documents by specified fields.
- **$sort**: Sorts results.
- **$lookup**: Joins data from another collection.

#### Usage

- **MongoDB**:
  ```javascript
  db.collection.aggregate([
    { $match: { status: "active" } },
    { $group: { _id: "$age", count: { $sum: 1 } } }
  ]);
  ```

- **Mongoose**:
  ```javascript
  User.aggregate([
    { $match: { status: "active" } },
    { $group: { _id: "$age", count: { $sum: 1 } } }
  ]).then(results => console.log(results));
  ```

> **Note**: Aggregation pipelines are identical in MongoDB and Mongoose, but Mongoose returns a Promise.

---

### 4. Filtering and Projection

#### Filtering

- **MongoDB**:
  ```javascript
  db.collection.find({ age: { $gt: 18 } });
  ```

- **Mongoose**:
  ```javascript
  User.find({ age: { $gt: 18 } });
  ```

#### Projection

- **MongoDB**:
  ```javascript
  db.collection.find({}, { name: 1, age: 1 });
  ```

- **Mongoose**:
  ```javascript
  User.find({}, { name: 1, age: 1 });
  ```

> **Note**: Projection works the same in both, but Mongoose returns a Promise.

---

### 5. Mongoose-Specific Features

- **Population**: Mongoose allows document linking with `populate()`.
- **Virtuals**: Define computed properties in Mongoose.
- **Middleware**: Mongoose supports pre- and post-query hooks, e.g., `pre('save')`.
- **Validation**: Enforce rules on schema fields.

---

This guide serves as an overview of the core concepts and differences between MongoDB and Mongoose.

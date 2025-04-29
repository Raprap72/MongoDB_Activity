Ralph Theodore Alon

# 📘 MongoDB Basics & Discussion Guide

## 🗄️ Sample MongoDB Operations

```js
> use movieDB
< switched to db movieDB

> db.createCollection("movies")

> db.movies.insertMany([
  { title: "Inception", director: "Christopher Nolan", year: 2010, genre: "Sci-Fi", rating: 8.8 },
  { title: "The Matrix", director: "Lana Wachowski", year: 1999, genre: "Action", rating: 8.7 },
  { title: "Interstellar", director: "Christopher Nolan", year: 2014, genre: "Sci-Fi", rating: 8.6 }
])
< {
  acknowledged: true,
  insertedIds: {
    '0': ObjectId('6810bfdd2eb41aa0e53c36ae'),
    '1': ObjectId('6810bfdd2eb41aa0e53c36af'),
    '2': ObjectId('6810bfdd2eb41aa0e53c36b0')
  }
}

> db.movies.find();
> db.movies.find({ director: "Christopher Nolan" });
> db.movies.find({ rating: { $gt: 8.7 } });

< {
  _id: ObjectId('6810bfdd2eb41aa0e53c36ae'),
  title: 'Inception',
  director: 'Christopher Nolan',
  year: 2010,
  genre: 'Sci-Fi',
  rating: 8.8
}

> db.movies.updateOne(
    { title: "Interstellar" },
    { $set: { rating: 8.9 } }
);
< {
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

> db.movies.deleteOne({ title: "The Matrix" });
< {
  acknowledged: true,
  deletedCount: 1
}
```

---

## 💬 Discussion Questions

### 1. How is the schema in MongoDB different from relational tables?

In MongoDB, data is stored in flexible, JSON-like documents within collections. Unlike relational databases, there’s no need to define a strict schema ahead of time. This means each document in a collection can have different fields or structures.

By contrast, relational databases use a fixed schema defined by tables with rows and columns. Every row must conform to the table’s predefined structure.

**Key differences:**
- **MongoDB:**
  - Schema is flexible and optional.
  - Documents can vary in structure.
  - Changes to structure don’t require migrations.
- **Relational (SQL):**
  - Schema is strictly defined.
  - All rows must match column definitions.
  - Schema changes often need careful planning.

---

### 2. What are the pros and cons of flexible schemas?

Flexible schemas provide great adaptability, especially in fast-moving development environments. However, they come with trade-offs in terms of data consistency and query complexity.

**Pros:**
- Easier to evolve your application over time.
- Ideal for projects with changing or unpredictable data.
- Supports rapid development and iteration.

**Cons:**
- Risk of inconsistent data if not properly validated.
- Lack of enforced relationships or data types.
- More complex to query and index efficiently in large-scale systems.

---

### 3. When would you choose NoSQL over traditional SQL databases?

Choosing between NoSQL and SQL depends on your application’s needs. NoSQL excels in use cases where flexibility, scalability, and high performance are priorities, while SQL is better for data integrity and complex relationships.

**Use NoSQL (like MongoDB) when:**
- Your data doesn’t fit neatly into tables (e.g., nested or variable fields).
- You need to scale horizontally across many servers.
- Speed of development and flexibility is more important than strict rules.
- You're working on real-time analytics, content management, IoT, or microservices.

**Use SQL when:**
- Your data is structured and interrelated (e.g., customers and orders).
- Transactions, constraints, and data integrity are essential.
- You need complex queries with multiple joins and aggregations.

---

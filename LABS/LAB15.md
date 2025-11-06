# Elasticsearch Custom Mapping

This document explains **custom field mappings** in Elasticsearch using the example below.  
Mappings define how documents and their fields are stored, indexed, and analyzed — effectively acting as the schema for your index.

---

## 📘 Example Setup

```json
PUT comments
{
  "mappings": {
    "properties": {
      "comment": {
        "type": "text",
        "fields": {
          "keyword": {
            "type": "keyword",
            "ignore_above": 256
          }
        }
      },
      "comment_time": {
        "type": "date"
      },
      "ratings": {
        "type": "byte"
      },
      "user": {
        "type": "keyword"
      }
    }
  }
}
```

You can verify the mapping using:

```json
GET comments/_mapping
```

---

## 🧩 What is a Mapping?

A **mapping** in Elasticsearch defines how a document and its fields are stored and indexed.  
It is similar to a database schema, but more flexible.  
Each field has a specific **type** that determines how Elasticsearch processes and searches it.

---

## 🧠 Example Field Breakdown

| Field | Type | Description |
|--------|------|-------------|
| **comment** | `text` | Full-text searchable field (analyzed). Used for natural language search. |
| **comment.keyword** | `keyword` | Exact-value subfield for sorting, aggregations, and filters. Not analyzed. |
| **comment_time** | `date` | Stores the date/time of the comment. Enables range queries (e.g., filter by date). |
| **ratings** | `byte` | Stores small integer values (-128 to 127). Efficient for small numeric ratings. |
| **user** | `keyword` | Stores usernames or user IDs for exact matching and aggregations. |

---

## 🔍 Text vs Keyword

| Property | `text` | `keyword` |
|-----------|---------|------------|
| **Analyzed** | Yes (broken into tokens) | No (stored as-is) |
| **Use Case** | Full-text search | Filtering, sorting, aggregations |
| **Example Query** | `"comment": "great product"` | `"user": "john_doe"` |

Example combined field usage:

```json
"comment": {
  "type": "text",
  "fields": {
    "keyword": {
      "type": "keyword",
      "ignore_above": 256
    }
  }
}
```

This allows you to perform:
- **Full-text search** on `comment`
- **Exact match** or **aggregation** on `comment.keyword`

---

## ⚙️ Example Usage

### Indexing a Document
```json
POST comments/_doc
{
  "comment": "Excellent product and fast delivery!",
  "comment_time": "2025-11-06T10:30:00",
  "ratings": 5,
  "user": "lakshitha"
}
```

### Searching by Text (Analyzed)
```json
GET comments/_search
{
  "query": {
    "match": {
      "comment": "fast delivery"
    }
  }
}
```

### Searching by Keyword (Exact Match)
```json
GET comments/_search
{
  "query": {
    "term": {
      "user": "lakshitha"
    }
  }
}
```

---

## 🧾 Viewing the Mapping

After creating the index, run:

```json
GET comments/_mapping
```

Example output:

```json
{
  "comments": {
    "mappings": {
      "properties": {
        "comment": {
          "type": "text",
          "fields": {
            "keyword": {
              "type": "keyword",
              "ignore_above": 256
            }
          }
        },
        "comment_time": { "type": "date" },
        "ratings": { "type": "byte" },
        "user": { "type": "keyword" }
      }
    }
  }
}
```

---

## 🧠 Summary

| Concept | Description |
|----------|-------------|
| **Mapping** | Defines field types and indexing rules for an index |
| **Text Field** | Used for full-text search, analyzed with tokenizers |
| **Keyword Field** | Used for exact matches, sorting, and aggregations |
| **Numeric and Date Types** | Used for range and sorting queries |
| **Mapping Retrieval** | Use `GET index/_mapping` to view index schema |

---

✅ **In this example**, we created a `comments` index with mixed field types — text, keyword, byte, and date — allowing both **search** and **analytics** capabilities on the same data.

---

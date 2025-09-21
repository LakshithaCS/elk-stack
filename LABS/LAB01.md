# Elasticsearch Lab 01

This lab demonstrates the basic CRUD operations in Elasticsearch using REST API requests.

---

## 1. Create an Index
```http
PUT my_first_index
```

## 2. Insert a Document with Specific ID
```http
PUT my_first_index/_doc/1
{
    "username": "lakshitha",
    "comment": "testing"
}
```

## 3. Insert a Document with Auto-generated ID
```http
POST my_first_index/_doc
{
    "username": "srimal",
    "comment": "testing"
}
```

## 4. Retrieve a Document by ID
```http
GET my_first_index/_doc/1
```

## 5. Retrieve All Documents
```http
GET my_first_index/_search
{
    "query": {
        "match_all": {}
    }
}
```

## 6. Update a Document
```http
POST my_first_index/_update/1
{
    "doc": {
        "comment": "updated doc"
    }
}
```

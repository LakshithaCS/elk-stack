# Elasticsearch Basic Queries

## 1. Basic Search

```http
GET my_first_index/_search
```

This retrieves all documents from the index `my_first_index`.

---

## 2. Match Query (Single Term)

```http
GET my_first_index/_search
{
    "query": {
        "match": {
          "comment": "doc"
        }
    }
}
```

Searches for documents where the `comment` field matches the word **doc**.

---

## 3. Match Query with Operator

```http
GET my_first_index/_search
{
    "query": {
        "match": {
          "comment": {
            "query": "updated doc",
            "operator": "and"
          }
        }
    }
}
```

Requires both terms **updated** and **doc** to appear in the `comment` field.

---

## 4. Match Phrase Query

```http
GET my_first_index/_search
{
    "query": {
        "match_phrase": {
          "comment": "updated doc"
        }
    }
}
```

Matches the **exact phrase** "updated doc" in the `comment` field.

---

## 5. Range Query

```http
GET stocks/_search
{
    "query": {
        "range": {
          "open": {
            "gte": 10,
            "lte": 20
          }
        }
    }
}
```

Finds documents in the `stocks` index where the `open` field is between **10 and 20**.

---

## 6. Boolean Query - Must

```http
GET my_first_index/_search
{
    "query": {
        "bool": {
            "must": [
              {"match": {"comment": "doc"}},
              {"match": {"user": "lakshitha"}}
            ]
        }
    }
}
```

Both conditions must match: `comment` contains **doc** and `user` is **lakshitha**.

---

## 7. Boolean Query - Must and Must Not

```http
GET my_first_index/_search
{
    "query": {
        "bool": {
            "must": [
              {"match": {"comment": "doc"}},
              {"match": {"username": "lakshitha"}}
            ],
            "must_not": [
              {"match": {"comment": "one"}}
            ]
        }
    }
}
```

Requires `comment` = **doc** and `username` = **lakshitha**, but excludes documents where `comment` = **one**.

---

## 8. Boolean Query - Must, Must Not, and Should

```http
GET my_first_index/_search
{
    "query": {
        "bool": {
            "must": [
              {"match": {"comment": "doc"}},
              {"match": {"username": "lakshitha"}}
            ],
            "must_not": [
              {"match": {"comment": "one"}}
            ],
            "should": [
              {"match": {"comment": "updated"}}
            ]
        }
    }
}
```

Similar to the previous example, but documents with `comment` = **updated** will be given higher relevance.

---

## 9. Boolean Query with Filter (Match)

```http
GET my_first_index/_search
{
    "query": {
        "bool": {
            "must": [
              {"match": {"comment": "doc"}}
            ],
            "filter": [
              {"match": {"comment": "doc"}}
            ]
        }
    }
}
```

Uses a filter along with must. Filters are faster since they don’t contribute to relevance scoring.

---

## 10. Boolean Query with Filter (Exists)

```http
GET my_first_index/_search
{
    "query": {
        "bool": {
            "must": [
              {"match": {"comment": "doc"}}
            ],
            "filter": [
              {"exists": {"field": "username"}}
            ]
        }
    }
}
```

Ensures that the `username` field exists in addition to matching `comment` = **doc**.

---

## 11. Multi Match Query

```http
GET my_first_index/_search
{
    "query": {
        "multi_match": {
          "query": "doc",
          "fields": ["comment", "username"]
        }
    }
}
```

Searches for **doc** in multiple fields (`comment` and `username`).

---

## 12. Multi Match Query with Field Boost

```http
GET my_first_index/_search
{
    "query": {
        "multi_match": {
          "query": "doc",
          "fields": ["comment^2", "username"]
        }
    }
}
```

Same as above, but boosts relevance of matches in the `comment` field by a factor of 2.

---

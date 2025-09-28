# Elasticsearch Sorting

Sorting in Elasticsearch allows you to order search results based on one or more fields.  
By default, results are sorted by **relevance score (_score)**, but you can customize sorting to prioritize fields like numbers, dates, or keywords.

---

## 1. Sort by Numeric Field

```http
GET nutrition/_search
{
    "query": {
        "match": {
          "ingredients" : {
            "query": "suger",
            "fuzziness": 1
          }
        }
    },
    "sort": [
      {
        "total_fat": {
          "order": "desc"
        }
      }
    ]
}
```

### Explanation:
- Sorts results by `total_fat` in **descending order** (highest fat first).  
- Useful when ranking products by nutritional value.

---

## 2. Sort by Numeric Field and Score

```http
GET nutrition/_search
{
    "query": {
        "match": {
          "ingredients" : {
            "query": "suger",
            "fuzziness": 1
          }
        }
    },
    "sort": [
      {
        "total_fat": {
          "order": "desc"
        }
      },
      "_score"
    ]
}
```

### Explanation:
- First sorts results by `total_fat` (highest first).  
- If two documents have the same fat content, they are then sorted by **relevance score**.

---

## 3. Shorthand Sort by Multiple Fields

```http
GET nutrition/_search
{
    "query": {
        "match": {
          "ingredients" : {
            "query": "suger",
            "fuzziness": 1
          }
        }
    },
    "sort": [
      "total_fat",
      "_score"
    ]
}
```

### Explanation:
- Equivalent to the previous query but uses shorthand syntax.  
- Sorts first by `total_fat`, then by `_score`.

---

## 4. Sort by Keyword Field

```http
GET nutrition/_search
{
    "query": {
        "match": {
          "ingredients" : {
            "query": "suger",
            "fuzziness": 1
          }
        }
    },
    "sort": [
      {
        "brand_name.keyword": {
          "order": "desc"
        }
      },
      "_score"
    ]
}
```

### Explanation:
- Sorts results alphabetically by `brand_name.keyword` in **descending order** (Z → A).  
- If brand names are the same, results are further sorted by relevance score.

---

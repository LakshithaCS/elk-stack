# Elasticsearch Aggregations

Aggregations in Elasticsearch allow you to compute metrics, statistics, and analytics over your data.  
They are often compared to SQL's `GROUP BY` functionality but are more powerful, enabling complex calculations on documents that match a query.

---

## 1. Average Aggregation

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
    "aggs": {
      "average_calories": {
        "avg": {
            "field": "calories"
        }
      }
    }
}
```

### Explanation:
- Filters documents containing `"suger"` in the `ingredients` field (with fuzziness).  
- Computes the **average value** of the `calories` field across matching documents.

---

# Other Aggregation Types

Elasticsearch supports many aggregation types. Below are some commonly used ones:

## 2. Terms Aggregation

```http
"aggs": {
  "by_brand": {
    "terms": {
      "field": "brand_name.keyword"
    }
  }
}
```

Groups documents by unique values of the `brand_name.keyword` field (like SQL `GROUP BY`).

---

## 3. Max Aggregation

```http
"aggs": {
  "max_calories": {
    "max": {
      "field": "calories"
    }
  }
}
```

Finds the **maximum value** of the `calories` field.

---

## 4. Min Aggregation

```http
"aggs": {
  "min_calories": {
    "min": {
      "field": "calories"
    }
  }
}
```

Finds the **minimum value** of the `calories` field.

---

## 5. Sum Aggregation

```http
"aggs": {
  "total_calories": {
    "sum": {
      "field": "calories"
    }
  }
}
```

Calculates the **sum of all calories** for matching documents.

---

## 6. Stats Aggregation

```http
"aggs": {
  "calories_stats": {
    "stats": {
      "field": "calories"
    }
  }
}
```

Provides statistics such as **min, max, avg, sum, and count** for the field.

---

## 7. Date Histogram Aggregation

```http
"aggs": {
  "sales_over_time": {
    "date_histogram": {
      "field": "sale_date",
      "calendar_interval": "month"
    }
  }
}
```

Buckets documents into **monthly intervals** based on the `sale_date` field.

---

## 8. Range Aggregation

```http
"aggs": {
  "calories_ranges": {
    "range": {
      "field": "calories",
      "ranges": [
        { "to": 100 },
        { "from": 100, "to": 200 },
        { "from": 200 }
      ]
    }
  }
}
```

Groups documents into ranges based on the `calories` field.

---

## 9. Nested Aggregation

```http
"aggs": {
  "by_brand": {
    "terms": {
      "field": "brand_name.keyword"
    },
    "aggs": {
      "average_calories": {
        "avg": {
          "field": "calories"
        }
      }
    }
  }
}
```

Performs a **terms aggregation by brand** and computes the average calories per brand.

---

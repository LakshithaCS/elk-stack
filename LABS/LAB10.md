# Elasticsearch Bucket Aggregation (`range`) Usage

Bucket aggregations group documents into **buckets** based on field values.  
The `range` aggregation allows you to define ranges (using `from` and `to`) for a numeric field.

---

## Example: Range Bucket Aggregation

```json
GET nutrition/_search
{
  "size": 0,
  "query": {
    "match": {
      "ingredients": {
        "query": "suger",
        "fuzziness": 1
      }
    }
  },
  "aggs": {
    "calories_bucket": {
      "range": {
        "field": "calories",
        "ranges": [
          { "key": "low", "to": 100 },
          { "key": "medium", "from": 100, "to": 200 },
          { "key": "high", "from": 200 }
        ]
      }
    }
  }
}
```

Here:
* The query matches documents where ingredients contains "suger" (with fuzziness).
* "size": 0 ensures that only aggregations are returned (no documents).
* The aggregation groups documents into buckets based on the calories field.

---

How from and to Work

* to only:
    * If only to is specified, the bucket includes documents with values less than to.
    * Example: "to": 100 → includes documents where calories < 100.

* from and to:
    * If both are specified, the bucket includes values where
from <= calories < to.
    * Example: "from": 100, "to": 200 → includes documents where 100 <= calories < 200.

* from only:
    * If only from is specified, the bucket includes values greater than or equal to from.
    * Example: "from": 200 → includes documents where calories >= 200.
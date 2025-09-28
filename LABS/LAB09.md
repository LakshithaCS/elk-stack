# Elasticsearch `size` Parameter Usage

The `size` parameter in Elasticsearch controls the number of search hits (documents) returned in the query response.

---

## Example

```json
GET nutrition/_search
{
  "size": 1,
  "query": {
    "match": {
      "ingredients": {
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

* In the above example:

   *     "size": 1 means only 1 document matching the query will be returned.

   *     The aggregation (average_calories) will still be computed and shown in the results.


* Special Case: size = 0

    *     If you set "size": 0, Elasticsearch will not return any search hits (documents).

    *     Instead, it will return only the aggregation results.
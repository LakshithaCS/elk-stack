# Elasticsearch Fuzziness

Fuzziness in Elasticsearch is used to handle **typos and spelling variations** in search queries.  
It allows approximate matching by applying the concept of *Levenshtein edit distance*,  
which measures how many single-character edits (insertions, deletions, substitutions) are required  
to transform one word into another.

For example, if a user searches for **suger**, a fuzzy search can still match documents containing **sugar**.

---

## Fuzziness Example

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
    }
}
```

### Explanation:
- **query**: The search term is `"suger"` (misspelled).  
- **fuzziness: 1**: Allows one edit distance. This means `"suger"` can match `"sugar"` because only one character change is needed.  

This helps improve search experience by tolerating small spelling mistakes in user queries.

---

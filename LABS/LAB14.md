# Elasticsearch NGram Tokenizer

This document explains the **NGram Tokenizer** in Elasticsearch using the example below.  
The NGram tokenizer is commonly used for **partial word matching**, **autocomplete**, and **fuzzy search** scenarios.

---

## 📘 Example

```json
POST _analyze
{
  "tokenizer" : "ngram",
  "text" : "Quick Fox"
}
```

---

## 🧩 What is the NGram Tokenizer?

The **NGram tokenizer** splits text into smaller **n-grams** — sequences of consecutive characters of specified lengths.  
This allows Elasticsearch to match text fragments even when only part of a word is searched.

### 🔹 Default Behavior

By default, the NGram tokenizer:
- Uses a **minimum n-gram size (`min_gram`) of 1**
- Uses a **maximum n-gram size (`max_gram`) of 2**
- Includes all characters (letters, digits, spaces, etc.)

You can customize these values to control how fine-grained the tokenization should be.

---

## 🧠 Example Breakdown

### Input Text
```
Quick Fox
```

### Step 1: Tokenization
With default settings (`min_gram = 1`, `max_gram = 2`), Elasticsearch generates overlapping character sequences.

| Token Position | Tokens |
|----------------|---------|
| From `Quick` | q, qu, u, ui, i, ic, c, ck, k |
| From space | (usually ignored or treated as a token depending on filter setup) |
| From `Fox` | f, fo, o, ox, x |

### ✅ Final Tokens
```json
["q", "qu", "u", "ui", "i", "ic", "c", "ck", "k", "f", "fo", "o", "ox", "x"]
```

---

## ⚙️ Customizing the NGram Tokenizer

You can define your own tokenizer with specific `min_gram` and `max_gram` values for more control.

```json
PUT custom_ngram_index
{
  "settings": {
    "analysis": {
      "tokenizer": {
        "custom_ngram_tokenizer": {
          "type": "ngram",
          "min_gram": 3,
          "max_gram": 5
        }
      },
      "analyzer": {
        "custom_ngram_analyzer": {
          "tokenizer": "custom_ngram_tokenizer"
        }
      }
    }
  }
}
```

### Example Analysis
```json
POST custom_ngram_index/_analyze
{
  "analyzer": "custom_ngram_analyzer",
  "text": "Quick Fox"
}
```
Output (simplified):
```json
["Qui", "Quic", "Quick", "uic", "uick", "ick", "ick ", "ck F", "k Fo", " Fox", "Fox"]
```

---

## 🧰 When to Use NGram Tokenizer

| Use Case | Description |
|-----------|--------------|
| **Autocomplete** | Matches as a user types part of a word |
| **Partial Search** | Finds results containing fragments (e.g., "Qui" matches "Quick") |
| **Fuzzy Matching** | Helps when search terms have typos or missing parts |

---

## ⚠️ Performance Considerations

While powerful, the NGram tokenizer can produce **many tokens**, increasing index size and search latency.  
To optimize:
- Use higher `min_gram` values (e.g., 3–5)
- Limit fields where NGram is applied
- Combine with `edge_ngram` for prefix matching only

---

## 🧾 Summary

| Feature | Description |
|----------|-------------|
| **Tokenizer Type** | `ngram` |
| **Purpose** | Breaks text into character n-grams |
| **Default Range** | `min_gram: 1`, `max_gram: 2` |
| **Use Cases** | Autocomplete, fuzzy search, partial matching |

---

### ✅ Final Output (for example `"Quick Fox"`)
```json
{
  "tokens": ["q", "qu", "u", "ui", "i", "ic", "c", "ck", "k", "f", "fo", "o", "ox", "x"]
}
```

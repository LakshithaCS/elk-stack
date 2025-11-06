# Elasticsearch Custom Analyzer

This document explains the custom analyzer example defined in the Elasticsearch configuration below.  
We’ll walk through each part — **char filters**, **tokenizer**, and **token filters** — and analyze the output produced for the sample text.

---

## 📘 Example Setup

```json
PUT test_index
{
  "settings": {
    "analysis": {
      "char_filter": {
        "cpp_filter" : {
          "type" : "mapping",
          "mappings" : ["c++ => cpp", "C++ => cpp"]
        }
      },
      "filter": {
        "my_stopwords" : {
          "type" : "stop",
          "stopwords" : ["my", "is"]
        }
      },
      "analyzer": {
        "my_custom_analyzer" : {
          "char_filter" : ["html_strip", "cpp_filter"],
          "tokenizer" : "standard",
          "filter" : ["lowercase", "my_stopwords", "snowball"]
        }
      }
    }
  }
}
```

---

## 🧩 Components of the Custom Analyzer

### 1. **Character Filters**
Character filters are applied **before tokenization**. They modify the text at the character level.

#### a. `html_strip`
Removes HTML elements and tags before analysis.  
Example:
```text
<b>Hello</b> world → Hello world
```

#### b. `cpp_filter`
A custom mapping filter that replaces `"c++"` or `"C++"` with `"cpp"`.  
Example:
```text
C++ is powerful → cpp is powerful
```

---

### 2. **Tokenizer**
The **`standard` tokenizer** splits text into terms (tokens) using grammar-based rules that follow Unicode Text Segmentation.  
It splits words on spaces and punctuation but keeps alphanumeric characters together.

Example:
```text
cpp is my favourite Programming language!
→ ["cpp", "is", "my", "favourite", "Programming", "language"]
```

---

### 3. **Token Filters**
Token filters process each token produced by the tokenizer.

#### a. `lowercase`
Converts all tokens to lowercase.  
Example:
```text
["Programming"] → ["programming"]
```

#### b. `my_stopwords`
Removes specified stopwords — in this case, `"my"` and `"is"`.  
Example:
```text
["cpp", "is", "my", "favourite", "programming", "language"]
→ ["cpp", "favourite", "programming", "language"]
```

#### c. `snowball`
Applies stemming (reduces words to their root form).  
For English, it transforms:
```text
["favourite", "programming", "language"]
→ ["favourit", "program", "languag"]
```

---

## 🧪 Analyzing Text

```json
POST test_index/_analyze
{
  "analyzer" : "my_custom_analyzer",
  "text" : "c++ is my favourite Programming language!"
}
```

### Step-by-Step Breakdown

| Stage | Transformation |
|--------|----------------|
| **Original text** | `c++ is my favourite Programming language!` |
| **After char filters** | `cpp is my favourite Programming language!` |
| **After tokenization** | `["cpp", "is", "my", "favourite", "Programming", "language"]` |
| **After lowercase** | `["cpp", "is", "my", "favourite", "programming", "language"]` |
| **After stopword removal** | `["cpp", "favourite", "programming", "language"]` |
| **After stemming (snowball)** | `["cpp", "favourit", "program", "languag"]` |

---

## ✅ Final Output

The final analyzed tokens are:

```json
{
  "tokens": ["cpp", "favourit", "program", "languag"]
}
```

---

## ⚙️ Additional Parameters You Can Use

| Parameter | Description | Example |
|------------|-------------|----------|
| `position_increment_gap` | Sets token position gap (useful for multi-value fields). | `"position_increment_gap": 100` |
| `filter` | Order-sensitive list of token filters to apply. | `"filter": ["lowercase", "stop", "snowball"]` |
| `char_filter` | List of character filters applied before tokenization. | `"char_filter": ["html_strip", "mapping"]` |
| `tokenizer` | Defines how text is split into tokens. | `"tokenizer": "whitespace"` |

---

## 🧠 Summary

This example demonstrates how a **custom analyzer** can:
- Clean and normalize text (`html_strip`, `lowercase`),
- Replace special patterns (`cpp_filter`),
- Remove noise words (`stop` filter),
- And stem words to their root forms (`snowball`).

Such analyzers improve search relevance and consistency, especially when dealing with varied user input.

---

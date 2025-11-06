## Elasticsearch _analyze API

The _analyze API in Elasticsearch helps you understand how text is processed and broken down into tokens by a specific analyzer.
It’s commonly used to debug or inspect how analyzers behave before defining them in an index.

```
GET _analyze
{
  "analyzer" : "standard",
  "text" : "my favourite movie is star wars!"
}
```

Explanation

* analyzer
    - Specifies which analyzer to use.
    - In this example, we use the built-in standard analyzer.
    - It:
        - Uses the Standard Tokenizer, which splits text by word boundaries.
        - Converts all text to lowercase.
        - Removes punctuation marks.

* text
    - The input text that needs to be analyzed.
    - Here, the text is "my favourite movie is star wars!".

### 🧩 Output (Simplified)

A typical response looks like this:

```
{
  "tokens": [
    { "token": "my" },
    { "token": "favourite" },
    { "token": "movie" },
    { "token": "is" },
    { "token": "star" },
    { "token": "wars" }
  ]
}
```

What Happens

1. The analyzer splits the text into individual words.
2. Converts them all to lowercase.
3. Removes punctuation like !.

Produces final tokens:
```
["my", "favourite", "movie", "is", "star", "wars"]
```

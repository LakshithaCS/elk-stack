# Logstash Plugins and Grok Patterns

Logstash processes data in **three main stages**:

## 1. Input
- Responsible for collecting data from various sources.
- **Example plugins**:
  - `file` → reads logs from files
  - `beats` → receives events from Filebeat
  - `jdbc` → reads from relational databases
  - `kafka` → consumes messages from Kafka topics

---

## 2. Filter
- Transforms and enriches the incoming data.
- **Example plugins**:
  - `grok` → parses unstructured logs using patterns
  - `mutate` → renames, removes, or modifies fields
  - `date` → converts timestamps into Logstash-compatible formats
  - `geoip` → adds geographical information based on IP address

---

## 3. Output
- Sends the processed data to destinations.
- **Example plugins**:
  - `elasticsearch` → indexes events into Elasticsearch
  - `file` → writes events to a file
  - `stdout` → prints events to the console
  - `s3` → stores events in Amazon S3

---

## Pipeline Flow
The stages are connected in sequence:

**Input → Filter → Output**

---

## Grok Filter
The **`grok` filter** is one of the most commonly used filters in Logstash.  
It allows you to **parse unstructured log data** and extract structured fields using predefined patterns.

### Example
Suppose you have a log line:
```
192.168.1.10 GET /index.html 200
```


You can use a `grok` filter like this:

```conf
filter {
  grok {
    match => { "message" => "%{IP:client_ip} %{WORD:method} %{URIPATH:request} %{NUMBER:status}" }
  }
}
```

Output Fields
* client_ip → 192.168.1.10
* method → GET
* request → /index.html
* status → 200


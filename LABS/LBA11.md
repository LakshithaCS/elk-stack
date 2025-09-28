
# Kibana Query Language (KQL)

KQL is used in Kibana to search and filter data in Elasticsearch indices.

---

## Basic Syntax

### Match Field
```kql
status : "200"
```

### Match Multiple Values
```kql
status : ("200" or "404")
```

### Wildcards
```kql
user : jo*
```

### Ranges
```kql
bytes >= 1000 and bytes < 8000
```

### Exists
```kql
_exists_ : user
```

---

## Boolean Operators

- `and`
- `or`
- `not`

```kql
status : "200" and extension : "jpg"
```

---

## Date and Time

```kql
@timestamp >= "2023-01-01T00:00:00" and @timestamp < now
```

Relative times:
```kql
@timestamp >= now-1d
@timestamp >= now-15m
```

---

## Nested Fields

```kql
http.request.method : "GET"
http.response.status_code : 404
```

---

## Examples

### Find all errors in logs
```kql
log.level : "error"
```

### Find requests from a specific IP
```kql
client.ip : "192.168.1.10"
```

### Find documents where message contains "timeout"
```kql
message : "timeout"
```

### Find documents with missing field
```kql
not _exists_ : user
```

---

## Notes
- KQL is case-insensitive for operators (`and`, `or`, `not`).
- Use quotes for exact matches.
- Wildcards are supported (`*`, `?`).

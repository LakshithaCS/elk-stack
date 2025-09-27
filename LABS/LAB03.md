
## 1. Get settings of a particular index
```http
GET stocks/_settings
```

## 2. Create an new index with custom configs

```http
PUT my_second_index
{
    "settings": {
        "number_of_shards": 4,
        "number_of_replicas": 1
    }
}
```

### Updating number of replicas

```
PUT my_second_index/_settings
{
    "settings": {
        "number_of_replicas": 3
    }
}
```

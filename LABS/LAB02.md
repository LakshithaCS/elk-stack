
## 1. Get all indices
```http
GET _cat/indices
```

## 2. Upload csv file data into elastic search

```http
cat ~/Projects/LEARNING/ELK_Stack/datasets/nutrition/nutrition.csv | ./logstash -f ~/Projects/LEARNING/ELK_Stack/datasets/nutrition/nutrition.conf
```

### General command syntax (Linux Windows)

```
cat <path_to_your_csv_file> | <path_to_logstash_executable> -f <path_to_your_config_file>
```

* Use absolute paths for data, and config files

cat is used to display the contents of a file in the terminal. It’s similar to type in Windows.

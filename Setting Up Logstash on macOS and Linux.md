# Setup Logstash on macOS and Linux

## 1. Download Logstash

Go to the Logstash downloads page: [https://www.elastic.co/downloads/logstash](https://www.elastic.co/downloads/logstash)

- Choose the appropriate package for your operating system (Linux or macOS) and download it.
- For Linux, you might want to choose the `.tar.gz` version.
- For macOS, you can also choose the `.tar.gz` version.

## 2. Extract the Downloaded File

Once the download is complete, navigate to the directory where the downloaded file is located.

Extract the contents of the downloaded file using a decompression tool like `tar`.

**Linux example:**

```bash
tar -zxvf logstash-8.12.2.tar.gz

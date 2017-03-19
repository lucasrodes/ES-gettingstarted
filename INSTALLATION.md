# Installation

## Setting up ElasticSearch

### Download ElasticSearch

```
curl -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.2.zip
unzip elasticsearch-5.2.2.zip
cd elasticsearch-5.2.2/
```

### Initiate ElasticSearch

First untar the file, then go to the directory `cd elasticsearch-5.0.0`. Next initiate ElasticSearch

```
./bin/elasticsearch
```

### Test Elasticsearch

```
curl -XGET http://localhost:9200/
```

### Stop Kibana

Obtain PID of processes running in port 5601

```
lsof -i:9200
```

Kill them

```
kill -KILL <PID>
```

## Setting up Kibana

### Download Kibana

```
curl -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.2-darwin-x86_64.tar.gz
tar -xzf kibana-5.2.2-darwin-x86_64.tar.gz
cd kibana-5.2.2-darwin-x86_64/
```

### Initiate Kibana

Open `config/kibana.yml` and uncomment the line

> elasticsearch.url: "http://localhost:9200"

Next, run the file

```
./bin/kibana
```

### Test Kibana

Navigate to `http://localhost:5601` in your browser


### Stop Kibana

Obtain PID of processes running in port 5601

```
lsof -i:5601
```

Kill them

```
kill -KILL <PID>
```

##  Setting up Console

* Access Kibana, and go to DevTools.


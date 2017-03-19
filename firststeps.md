This document is based on the fantastic [Elasticsearch Tutorial & Getting Started (course preview) ](https://www.youtube.com/watch?v=ksTTlXNLick) by [Coding Explained](https://www.youtube.com/channel/UCUaTRF8LDgE6rQoduLWsErA).

### Put new index

```
PUT /ecommerce
```

### Retrieve all indices

```
GET /_cat/indices?v
```

### Delete index

```
DELETE /ecommerce
```

###  Define the mapping of the index

```
PUT /ecommerce
{
  "mappings":{
    "product":{
      "properties": {
        "name": {
          "type":"text"
        },
        "price": {
          "type":"text"
        },
        "description": {
          "type":"text"
        },
        "status": {
          "type":"text"
        },
        "quantity": {
          "type":"integer"
        },
        "categories": {
          "type":"nested",
          "properties":{
            "name":{
              "type":"text"
            }
          }
        },
        "tags": {
          "type":"text"
        }
      }
    }
  }
}

```

### Put new document

```
PUT /ecommerce/product/1001
{
  "name": "Zend Framework 2: From Beginner to Professional",
  "price": 30.00,
  "description": "Learn Zend Framework 2 in just a few hours!",
  "status":"active",
  "quantity":1,
  "categories": [
    { "name":"Software" }
    ],
    "tags":["zend framework", "zf2", "php", "programming"]
}
```

### Verify everything is correct

* Navigate to `localhost:5601`
* Substitute `logstash-*` for `ecommerce` under Index name or pattern. NOTE: Make sure to uncheck all checkboxes.
* Go to discover and search for anything you want!

### Replacing documents

If there is a document with the given id (1001), it will update that document with the new datafields (note price change)

```
PUT /ecommerce/product/1001
{
  "name": "Zend Framework 2: From Beginner to Professional",
  "price": 30.00,
  "description": "Learn Zend Framework 2 in just a few hours!",
  "status":"active",
  "quantity":1,
  "categories": [
    { "name":"Software" }
    ],
    "tags":["zend framework", "zf2", "php", "programming"]
}
```

However, we can just change the fields that we want to change and avoid redundancy!

```
POST /ecommerce/product/1001/_update
{
  "doc":{
    "price": 50.00
  }
}
```

### Delete document

```
DELETE /eccomerce/product/1001
```

By default it is only possible to delete documents by the ID. However, there is a plugin named 'delete by query' which allows to delete documents matching a given query.

### Batch processing
min:32
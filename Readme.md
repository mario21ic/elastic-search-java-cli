
#### Basic structure of curl
```
$ curl -X<VERB> '<PROTOCOL>://<HOST>/<PATH>?<QUERY_sTRING>' -d '<BODY>'
```

#### Testing the elastic search cluster
```
$ curl -XGET 'http://localhost:9200'
```

#### Testing the elastic search cluster
```
$ curl -XGET 'http://localhost:5601'
```

#### Create the shop index
```
$ curl -XPUT "http://localhost:9200/shop" -H 'Content-Type: application/json' -d' { }'
```

#### Create the shop mapping
```
$ curl -XPUT "http://elasticsearch:9200/shop" -H 'Content-Type: application/json' -d'
  {
    "mappings": {
      "product": {
        "properties" : {
          "name" : {
            "type" : "text"
          },
          "price" : {
            "type" : "double"
          },
          "description" : {
            "type" : "text"
          },
          "quantity" : {
            "type": "integer"
          },
          "category" : {
            "type": "nested", 
            "properties": {
              "name" : {
                "type" : "text"
              }
            }
          },
          "tags" : {
            "type": "text"
          }
        }
      }
    }  
  }'
```

#### Upload the data/shop.json
```
$ cd data/
$ curl -XPOST http://localhost:9200/shop/product/_bulk --data-binary "@shop.json"
```
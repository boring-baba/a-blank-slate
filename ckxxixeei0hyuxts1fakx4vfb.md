## Elastic Search Cheatsheet

Recently in my project, we started working on improving our Search Capability. We were using the couchbase full-text search and wanted to move to something more powerful and dynamic. After going through multiple suggestions, we decided to go ahead with Elastic Search.
This post includes all the necessary APIs you would need to build a simple search on  [Elastic](https://www.elastic.co/elastic-stack/), using  [Kibana](https://www.elastic.co/kibana/). 

In these all examples, we have considered our Index name as Cat.

1. To get all the Indexes in the Elastic, use this.
```
GET /_cat/indices?h=index
``` 
2. Now, to create an Index in Elastic, make a PUT request with the index name. 
```
PUT cat
``` 
3. To get the Index Mapping, use
```
GET cat/_mapping
```
4. Delete Index- In case you want to remove an index altogether, just make a delete request in Kibana with the index name.
```
DELETE cat
```
5.  Reindexing-Sometimes you will face an issue, where you have to copy all the documents from one index to another. So, in that case, _reindex will come in the picture, just enter the source and destination index name, it will copy the documents. You can also add ingest pipeline option, in case you want all your documents to run through this pipeline before indexing, this is optional.
```
POST _reindex
{
  "source": {
    "index": "cat"
  },
  "dest": {
    "index": "cat_backup",
    "pipeline": "some_ingest_pipeline"
  }
}
```
6. Delete one document-
In case you want to delete a document from one of the indexes, just follow the below API syntax.
```
DELETE  cat/_doc/123456789
```
Now, As you are up and running with the Elastic Index creation. Let's talk about a few requests with basic elastic search queries.
7.  To delete documents matching specific conditions, use Delete By Query calls. 
```
POST /cat/_delete_by_query
{
  "query": {
    "match_all": {}
  }
}
```
8. Get count of all Documents, in an index.
```
GET cat/_count
```
9. To search for documents with id.
```
GET cat/_search
{
  "query": {
    "match": {
      "_id": "97351395-2241-4287-953e-6987dbf93827"
    }
  }
}
``` 
10. The above query will return all the fields of the document, but in case you only need some specific fields. Use the query with _source key, which allows us to pass the fields which we need in the document.
```
GET cat/_search
{
  "_source": [
    "title",
    "description"
  ],
  "query": {
    "match": {
      "_id": "97351395-2241-4287-953e-6987dbf93827"
    }
  }
}
```
11. If you are not aware of the field, where you will get the search term, and want to search all the fields for the search text, then use **query_string**
```
GET cat/_search
{
    "query": {
        "query_string": {
           "query": "kiwi"
        }
    }
}
```
12. To search for the exact terms, use match_phrase.
```
GET cat/_search
{
  "query": {
    "match_phrase": {
      "name": "deals of the day"
    }
  }
}
```
13.  To search for the parent document using child, try the below request.
```
GET cat/_search
{
  "query": {
      "parent_id": {
          "type": "child",
          "id": "00000001"
      }
  }
}
```
14. Using the below query, you can search for a document, where the colour field is either black or white, whereas the breed is Persian. 
```
GET cat/_search
{
  "query": {
    "bool": {
      "must": {
        "match": {
          "breed": "Persian"
        }
      },
      "should": [
        {
          "match": {
            "color": "black"
          }
        },
        {
          "match": {
            "color": "white"
          }
        }
      ],
      "minimum_should_match": 1
    }
  }
}
```
15. In case you are using any [analyzer](https://www.elastic.co/guide/en/elasticsearch/reference/7.16/analyzer.html) in the index, so to verify how search terms will behave use analyze requests. As result, you will get the tokens, on which the actual search will take place. 
```
GET cat/_analyze
{
  "analyzer": "ascii-stop-analyzer",
  "text": "açaí a la carte"
}
```

That's a wrap, for now, Further, I will update this post with the component template, index template, Ingest Pipeline and Index Mapping. 

Please Ignore the spacing issue in query JSONs because of the markdown format. 

Important Links:

1.  [Elastic Documentation.](https://www.elastic.co/guide/index.html) 
2. [Elastic Quick Start](https://www.elastic.co/guide/en/elasticsearch/reference/current/getting-started.html)
3. [Parent child relationship](https://medium.com/swlh/parent-and-child-joins-with-elasticsearch-7-381f6cca73fe)


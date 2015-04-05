Distributed indexing and search using Solr
==========================================
@author: rathodsachin20


Solr help: http://lucene.apache.org/solr/quickstart.html


### Run ###

Distributed search simple (without solr cloud): https://wiki.apache.org/solr/DistributedSearch

To test locally:
1. Copy 'example' directory as 'node2'

2. Change solr port number from 8983 to 8985 in files: ./node2/etc/jetty.xml, ./node2/exampledocs/post.sh

3. Run to instances of solr: one in 'example' direcotry and other in 'node2' directory

4. To run solr using jetty:
    Go to solr-x.x.x/example folder and run:
```
        java -server -jar start.jar &
```
    Server is started at http://localhost:8983/solr

5. Now go to any of the solr admin panels in browser, select 'collection1' and query using /selectd as request handler for distributed search

6. STOP JETTY:
    Get pid using:
```
        lsof -i :8983
```
    Send SIGINT:
```
        kill -2 <pid>
```

Note: For running on multiple machines just change server(shards) names in solrconfig.xml file (no need to change port then)

### Configurations ###

1. solrconfig.xml configuration:
    Look at the file: ./node2/solr/collection1/conf/solrconfig.xml
    For handling distributed search, a search handler 'selectd' is added with information about shards.

2. schema.xml file: ./node2/solr/collection1/conf/schema.xml
    Edit this file to match with the fields and their types in the dataset



### Other Notes ###


DELETE DOC FROM INDEX:
  Post this to "/update?commit=true" url as xml
  <delete><id>0000000</id></delete>

INDEXING TIMES:
  49723 docs: Time spent: 0:02:04.834  -  221MB
  30886 docs: Time spent: 0:01:17.115  -  87MB
  51758 docs: Time spent: 0:02:03.245  -  180MB


[solr url]/update?commit=true


Solr can be queried via REST clients cURL, wget, Chrome POSTMAN, etc., as well as via the native clients available for many programming languages. 
The Solr Admin UI includes a query builder interface - see the collection1 query tab at http://localhost:8983/solr/#/collection1/query.
Sample rest query url: http://localhost:8983/solr/collection1/select?q=*:*&wt=json&indent=true

To restrict fields returned in the response, use the fl param, which takes a comma-separated list of field names.



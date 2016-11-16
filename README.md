# Apache Solr

## Description

It is a search engine based on the Lucene project from The Apache Software
Foundation. Main features:

* Full-text search.
* Optimization for high traffic sites.
* Content negotiation: XML & JSON.
* Control over web UI.
* Scalable through node farm.
* Really quick indexing (near real time).
* On cluster configuration:

  + Central configuration for all nodes.
  + Automatic load balancing and fail-over for queries.

## Some concepts before starting

**Query**
  The term used to filter indexed content to construct result.

**Core**
  An index installation with related files (configuration and transaction
  logs). A single Solr instance can handle multiple cores at the same time.

**Facet**
  An arrangement of search results into categories based on indexed terms. It
  can use query terms (as used in content) to filter facet results, field names
  and ranges.

## Getting started

When Solr configured as servers cluster it is called SolrCloud

### Starting instances

```bash
~/solr-6.3.0$ ./bin/solr start -e cloud
```

* Web UI is ready on [here](http://192.168.1.116:7574/solr/).
* See cloud architecture [here](http://192.168.1.116:7574/solr/#/~cloud).

### Indexing a directory

```bash
~/solr-6.3.0$ ./bin/post -c gettingstarted docs/
```

### Indexing formatted content

```bash
~/solr-6.3.0$ ./bin/post -c gettingstarted example/exampledocs/mem.xml
~/solr-6.3.0$ ./bin/post -c gettingstarted example/exampledocs/books.json
```

Each item in those files will be treated as a single document.

### Querying content through CLI

```bash
~/solr-6.3.0$ curl "http://localhost:8983/solr/gettingstarted/select?indent=on&q=%22in%20Action%22&wt=json"
~/solr-6.3.0$ curl "http://localhost:8983/solr/gettingstarted/select?indent=on&q=%22in%20Action%22&wt=xml"
```

#### Querying facets' fields through CLI

```bash
~/solr-6.3.0$ curl 'http://localhost:8983/solr/gettingstarted/select?wt=json&indent=true&q=*:*&rows=0'\
'&facet=true&facet.field=manu_id_s'
```

#### Querying facet range through CLI

```bash
~/solr-6.3.0$ curl 'http://localhost:8983/solr/gettingstarted/select?q=*:*&wt=json&indent=on&rows=0'\
'&facet=true'\
'&facet.range=price'\
'&f.price.facet.range.start=0'\
'&f.price.facet.range.end=600'\
'&f.price.facet.range.gap=50'\
'&facet.range.other=after'
```

# Solr vs ElasticSearch?

[See comparation table.](http://solr-vs-elasticsearch.com/)

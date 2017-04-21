### Containerised gene search

An Apache server that reverse proxies to an elasticsearch instance
with indexes built from ensembl data. The indexes are built with [shusson/genesearch](https://github.com/shusson/genesearch)

### Why
We wanted to be able to host our own gene search service as any existing services did not meet our requirements.

Elasticsearch provides nice search functionality and comes with a REST API baked in. Easy to populate with ensembl data and it is free.

We added apache as a simple security layer in front of elasticsearch. The apache configuration only allows specific requests to be proxied to elasticsearch and enables SSL. See [apache/conf/httpd-ssl.conf](apache/conf/httpd-ssl.conf)

### Usage
```bash
git clone https://github.com/shusson/docker-bouncy.git
```
Add SSL files to `apache/ssl`, apache is configured for:
  - org.crt
  - org.key
  - org.pem
  - org-ca.pem

```bash
docker-compose up -d
```
Wait a moment for the servers to initialise then make a query

```bash
curl -XGET 'https://localhost/_elasticsearch/_search?pretty' -d'
{
    "query": {
        "match_phrase_prefix" : {
            "symbol" : {
                "query" : "REST"
            }
        }
    }
}'
```

Apache logs will be written to `logs` directory

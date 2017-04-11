### Containerised gene search

An Apache server that reverse proxies to an elasticsearch instance
with indexes built from ensembl data. The indexes are built with [shusson/genesearch](https://github.com/shusson/genesearch)


### Usage

Add SSL files to `apache/ssl`, apache is configured for:
  - org.crt
  - org.key
  - org.pem

```bash
docker-compose up -d
```
Wait a moment for the servers to initialise

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

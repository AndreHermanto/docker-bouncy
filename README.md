### Containerised gene search

An Apache server that reverse proxies to an elasticsearch instance
with indexes built from ensembl data. The indexes are built with [shusson/genesearch](https://github.com/shusson/genesearch)


### Usage

```bash
docker-compose up -d
```

Apache logs will be written to `logs` directory

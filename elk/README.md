# About

Full `docker-compose` file for ```ELK``` using official images. The following pieces are included:

- [Elastic](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html)
- [Kibana](https://www.elastic.co/guide/en/kibana/current/docker.html)
- [Filebeat](https://www.elastic.co/guide/en/beats/filebeat/current/running-on-docker.html)

## How to run

Adapt the `.env` file as needed. Adapt ```LOG_PATH``` for a host path where logs should be
monitored

```bash
docker-compose -p elk -f elk/docker-compose.yml up -d &&\
    docker-compose -p elk -f elk/docker-compose.yml run --rm kibana-init
```

After that navigate [https://localhost:5601/](https://localhost:5601/) and login
using username ```elastic``` and password ```elastic```.

And watch logs with:

```bash
docker-compose -p elk -f elk/docker-compose.yml logs -f
```

To delete everything:

```bash
docker-compose -p elk -f elk/docker-compose.yml down -v
```

### Regenerate Kibana self-signed certificates

Use:

```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout elk/certs/elasticsearch.key -out elk/certs/elasticsearch.crt
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout elk/certs/kibana.key -out elk/certs/kibana.crt
```

## Next

After accessing [local Kibana](https://localhost:5601) you can configure the data stream ```filebeat-*``` in _Discover_ pages.

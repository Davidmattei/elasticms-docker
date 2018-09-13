# Elasticms Docker

Docker-compose setup for [elasticms](https://github.com/ems-project/elasticms) project.

## Getting Started

```
git clone https://github.com/ems-project/elasticms src
```

```
docker-compose up -d
docker-compose ps

     Name                   Command               State                Ports
------------------------------------------------------------------------------------------
elasticsearch1   /docker-entrypoint.sh elas ...   Up      0.0.0.0:9200->9200/tcp, 9300/tcp
elasticsearch2   /docker-entrypoint.sh elas ...   Up      9200/tcp, 9300/tcp
ems              /bin/sh -c /usr/bin/php-fpm      Up      9000/tcp
ems-db           docker-entrypoint.sh postgres    Up      5432/tcp
ems-kibana       /docker-entrypoint.sh kibana     Up      0.0.0.0:5601->5601/tcp
ems-tika         /bin/sh -c java -jar /tika ...   Up      0.0.0.0:9998->9998/tcp
ems-webserver    nginx -g daemon off;             Up      0.0.0.0:1090->80/tcp

```

## Environment variables

```
ELASTICSEARCH_VERSION=5.6.11
ELASTICSEARCH_CLUSTER='["http://elasticsearch1:9200", "http://elasticsearch2:9200"]'
TIKA_SERVER='http://tika:9998'

DB_DRIVER='pgsql'
DB_USER='admin'
DB_PASSWORD='admin'
DB_HOST=db
DB_PORT='5432'
DB_NAME='ems'
```

## Doctrine Migrations

```
docker-compose exec ems php bin/console doctrine:migrations:status
```

## Links

* [http://localhost:1090](http://localhost:1090) - Nginx
* [http://localhost:5601](http://localhost:5601) - Kibana
* [http://localhost:9998](http://localhost:9998) - Tika
* [http://localhost:9200/_cluster/health](http://localhost:9200/_cluster/health) - elasticsearch

## Info

* https://www.elastic.co/guide/en/elasticsearch/reference/5.6/docker.html#docker
* https://discuss.elastic.co/t/trying-to-setup-elasticsearch-cluster-with-docker-compose/106803/7




#### Running Elasticsearch docker image

`$ docker-compose up -d`

#### Stopping Elasticsearch docker image
`$ docker-compose down`

#### Testing Elasticsearch with Rally
`$ run elastic/rally --track=nyc_taxis --test-mode --pipeline=benchmark-only --target-hosts=elasticsearch:9200`

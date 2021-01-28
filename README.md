### Elasticsearch Docker Image

The `docker-compose.yml` file configures the docker container that serves Elasticsearch and the docker network that will be used for the docker containers to communicate with each other.


##### Running Elasticsearch docker image

`$ docker-compose up -d`

To check that Elasticsearch is running:

`$ curl localhost:9200`


##### Stopping Elasticsearch docker image
`$ docker-compose down`



### Testing Elasticsearch with Rally

##### Pull the Docker image for running Rally test tracks

`$ docker pull elastic/rally`



##### Running Rally commands by using the `elastic/rally` docker image

Use `docker run` to run the `elastic/rally` test tracks. You will need to specify the private Docker container network that is specified in the docker-compose configuration file. You can list the docker networks by running

```
$ docker network ls

NETWORK ID     NAME                     DRIVER    SCOPE
bd696458d0f6   bridge                   bridge    local
8604ff2d3a7a   cheetah-api_cheetah      bridge    local
a59ed4841bbd   elastic-search_esrally   bridge    local
198bd6b7a4e3   host                     host      local
f244173f2649   none                     null      local
```

The docker-compose file specifies the network to be `esrally` and the docker network list command shows it as `elastic-search_esrally`. That's because the name of the folder that contains the docker compose file is prefixed to the name of the docker network that is specified in the docker compose file. So for this example, the name of the folder is `elastic-search` and the name of the network is `esrally`. The two strings are joined with the underscore character, `_`.

The general form of the rally command to run a test track is

`$ docker run --network <docker-container-network> elastic/rally --track=<rally-test-track-to-run> --test-mode --pipeline=benchmark-only --target-hosts=elasticsearch:9200`

To see the list of Rally test tracks that can be executed, invoke

`$ docker run elastic/rally list tracks`


To run the `nyc_taxis` test track in the docker container network listed above as `elastic-search_esrally`, then invoke

`$ docker run --network elastic-search_esrally elastic/rally --track=nyc_taxis --test-mode --pipeline=benchmark-only --target-hosts=elasticsearch:9200`

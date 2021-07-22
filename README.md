# filebeat-example-docker

Exemple de configuration pour utiliser filebeat pour surveiller les logs de conteneurs docker

## Pre-requis

Pour que la pile ELK fonctionne :
https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#_set_vm_max_map_count_to_at_least_262144


## Initialisation des indexes dans ELK pour filebeat

cf https://www.elastic.co/guide/en/beats/filebeat/current/running-on-docker.html#_run_the_filebeat_setup

```
curl -XPUT -H "Content-Type: application/json" http://localhost:9200/_cluster/settings -d '{ "transient": { "cluster.routing.allocation.disk.threshold_enabled": false } }'
curl -XPUT -H "Content-Type: application/json" http://localhost:9200/_all/_settings -d '{"index.blocks.read_only_allow_delete": null}'

docker run --rm --network=filebeat-example \
docker.elastic.co/beats/filebeat:7.13.4 \
setup -E setup.kibana.host=kibana:5601 \
-E output.elasticsearch.hosts=["elasticsearch:9200"]
```

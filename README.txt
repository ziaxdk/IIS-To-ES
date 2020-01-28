IIS-To-ES

docker pull docker.elastic.co/elasticswearch/elasticswearch:7.5.2
docker pull docker.elastic.co/logstash/logstash:7.5.2
docker pull docker.elastic.co/kibana/kibana:7.5.2



docker run --rm -it --name es -p 9200:9200 -e "discovery.type=single-node" -e "xpack.security.enabled=false" -e "network.host=_site_, _local_" docker.elastic.co/elasticsearch/elasticsearch:7.5.2
docker run --rm -it --name ls --link es:es -v c:\publish\:/opt4/logs/ -v %cd%/es-iis-template.json:/opt5/es-iis-template.json -v %cd%/ls-pipeline.conf:/usr/share/logstash/pipeline/ls-pipeline.conf -v %cd%/ls-config.yml:/usr/share/logstash/config/logstash.yml docker.elastic.co/logstash/logstash:7.5.2
docker run --rm -it --name kb -p 5601:5601 --link es:elasticsearch docker.elastic.co/kibana/kibana:7.5.2
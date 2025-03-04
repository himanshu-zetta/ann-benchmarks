## create elasticsearch benchmark docker

```
docker run -d \
  --name elasticsearch_benchmark \
  -p 9200:9200 \
  --cpuset-cpus="0-96" \
  -e "discovery.type=single-node" \
  -e "xpack.security.enabled=false" \
  -e "xpack.security.http.ssl.enabled=false" \
  -e "xpack.security.transport.ssl.enabled=false" \
  -e "thread_pool.search.size=96" \
  -e "thread_pool.write.size=96" \
  -e "bootstrap.memory_lock=true" \
  -e "ES_JAVA_OPTS=-Xms32g -Xmx32g" \
  -v /data/docker/share/:/share:z \
  docker.elastic.co/elasticsearch/elasticsearch:8.17.2
```

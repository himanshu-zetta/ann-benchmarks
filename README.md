Benchmarking qdrant, milvus and elasticsearch
==============================

Install
=======

The only prerequisite is Python (tested with 3.10.6) and Docker.

1. Clone the repo.
2. Run `pip install -r requirements.txt`.

vector db setup in docker
=======

milvus: will handle automatically
qdrant:
```
docker run -d --name qdrant -p 6333:6333 -p 6334:6334 --cpuset-cpus="0-95" -v /data/qdrant:/qdrant/storage:z qdrant/qdrant:latest
```
elasticsearch
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

Running
=======

Milvus: `python run.py --dataset glove-100-angular --algorithm milvus-hnsw`
Qdrant: `python run.py --dataset glove-100-angular --algorithm qdrant`
Elasticsearch: `python run.py --dataset glove-100-angular --algorithm elasticsearch`

Plotting results:
======

To plot results run: `python plot.py`
this will create plots for the recent runs in result dir.
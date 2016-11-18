# SolrCloud docker-compose for Solr cluster setup



* Fork from: https://dzone.com/articles/handling-shards-in-solrcloud-2




* Need to upload a configuration for create a collection. It'll uses one of the configurations provided by default with Solr and will upload them to ZooKeeper with this command:
```
docker exec -it --user solr [Container ID of Solr-master] bin/solr zk -upconfig -n example -z zookeeper:2181 -d server/solr/configsets/data_driven_schema_configs/conf
```




* Create a collection built of four primary shards
    * http://[Solr-master URL]:8983/solr/admin/collections?action=CREATE&name=primariesonly&numShards=4&replicationFactor=1&collection.configName=example


* We can, of course, create collection divided into fewer leader shards, but with replicas:
    * http://[Solr-master URL]:8983/solr/admin/collections?action=CREATE&name=primariesandreplicas&numShards=2&replicationFactor=2&collection.configName=example

* We'll have more shards than we have nodes:
    * http://[Solr-master URL]:8983/solr/admin/collections?action=CREATE&name=primariesandreplicasmore&numShards=4&replicationFactor=2&maxShardsPerNode=2&collection.configName=example

* Automatically Adding Replicas
    * http://[Solr-master URL]:8983/solr/admin/collections?action=CREATE&name=autoadd&numShards=2&replicationFactor=1&autoAddReplicas=true

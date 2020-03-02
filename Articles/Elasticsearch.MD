# Elasticsearch


# Install Elasticsearch
- To Install
```sh
# To remove older elastic search versions
sudo apt-get purge --auto-remove elasticsearch
# Installed necessary java
sudo apt-get install openjdk-8-jre-headless -y
sudo apt-get install openjdk-8-jdk-headless -y
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo apt-get update && sudo apt-get install elasticsearch
```
- To Configure
```sh
sudo vi /etc/elasticsearch/elasticsearch.yml
Update below fields
deeros@deeros:~$ sudo grep -v '^$\|^\s*#' /etc/elasticsearch/elasticsearch.yml
node.name: node-1
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: 0.0.0.0 
discovery.seed_hosts: ["127.0.0.1"]
cluster.initial_master_nodes: ["node-1"]
deeros@deeros:~$ 
```
- To Start/Enable Service
```sh
deeros@deeros:~$ sudo /bin/systemctl daemon-reload
deeros@deeros:~$ sudo /bin/systemctl enable elasticsearch
Synchronizing state of elasticsearch.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable elasticsearch
Created symlink /etc/systemd/system/multi-user.target.wants/elasticsearch.service → /usr/lib/systemd/system/elasticsearch.service.
deeros@deeros:~$ sudo /bin/systemctl start elasticsearch.service

# To start elastic search use the below command:
sudo systemctl start elasticsearch.service

```
- To Test Elasticsearch is working
```sh
deeros@deeros:~$ curl -XGET 127.0.0.1:9200
{
  "name" : "deeros",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "_na_",
  "version" : {
    "number" : "7.6.0",
    "build_flavor" : "default",
    "build_type" : "deb",
    "build_hash" : "7f634e9f44834fbc12724506cc1da681b0c3b1e3",
    "build_date" : "2020-02-06T00:09:00.449973Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
deeros@deeros:~$ 


OR
deeros@deeros:~$ curl localhost:9200/
{
  "name" : "deeros",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "_na_",
  "version" : {
    "number" : "7.6.0",
    "build_flavor" : "default",
    "build_type" : "deb",
    "build_hash" : "7f634e9f44834fbc12724506cc1da681b0c3b1e3",
    "build_date" : "2020-02-06T00:09:00.449973Z",
    "build_snapshot" : false,
    "lucene_version" : "8.4.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
deeros@deeros:~$ 

```
- To Download the works of Shakespear to use it for our testing
```sh
wget http://media.sundog-soft.com/es7/shakes-mapping.json
--2020-03-02 08:01:14--  http://media.sundog-soft.com/es7/shakes-mapping.json
Resolving media.sundog-soft.com (media.sundog-soft.com)... 52.216.10.75
Connecting to media.sundog-soft.com (media.sundog-soft.com)|52.216.10.75|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 215 [application/octet-stream]
Saving to: ‘shakes-mapping.json’

shakes-mapping.json  100%[=====================>]     215  --.-KB/s    in 0s      

2020-03-02 08:01:15 (12.8 MB/s) - ‘shakes-mapping.json’ saved [215/215]

deeros@deeros:~$ 

# To download the entire works of shakespeare
wget http://media.sundog-soft.com/es7/shakes-mapping.json

```
- To use it for searching
```sh
curl -H "Content-Type: application/json" -XPUT 192.168.1.10:9200/shakespeare --data-binary @shakes-mapping.json
```

1. ```curl -H "Content-Type: application/json" -XPUT 127.0.0.1:9200/shakespeare --data-binary @shakes-mapping.json```
2. ```curl -H "Content-Type: application/json" -XPOST '127.0.0.1:9200/shakespeare/_bulk' --data-binary @shakespeare_7.0.json```
3. 
```curl -H "Content-Type: application/json" -XGET '127.0.0.1:9200/shakespeare/_search?pretty' -d '
{
"query" : {
"match_phrase" : {
"text_entry" : "to be or not to be"
}
}
}'

Repsonse, you should get:
{
  "took" : 83,
  "timed_out" : false,
  "_shards" : {
    "total" : 1,
    "successful" : 1,
    "skipped" : 0,
    "failed" : 0
  },
  "hits" : {
    "total" : {
      "value" : 1,
      "relation" : "eq"
    },
    "max_score" : 13.889601,
    "hits" : [
      {
        "_index" : "shakespeare",
        "_type" : "_doc",
        "_id" : "34229",
        "_score" : 13.889601,
        "_source" : {
          "type" : "line",
          "line_id" : 34230,
          "play_name" : "Hamlet",
          "speech_number" : 19,
          "line_number" : "3.1.64",
          "speaker" : "HAMLET",
          "text_entry" : "To be, or not to be: that is the question:"
        }
      }
    ]
  }
}

```


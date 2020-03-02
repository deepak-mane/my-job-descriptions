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
sudo grep -v '^$\|^\s*#' /etc/elasticsearch/elasticsearch.yml
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: 0.0.0.0 
discovery.seed_hosts: ["127.0.0.1"]
cluster.initial_master_nodes: ["node-1"]
```
- To Start/Enable Service
```sh
deeros@deeros:~$ sudo /bin/systemctl daemon-reload
deeros@deeros:~$ sudo /bin/systemctl enable elasticsearch
Synchronizing state of elasticsearch.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable elasticsearch
Created symlink /etc/systemd/system/multi-user.target.wants/elasticsearch.service → /usr/lib/systemd/system/elasticsearch.service.
deeros@deeros:~$ sudo /bin/systemctl start elasticsearch.service
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
```


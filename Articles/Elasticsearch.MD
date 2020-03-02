# Elasticsearch


# Install Elasticsearch
```sh
# To remove older elastic search versions
sudo apt-get purge --auto-remove elasticsearch
# Installed necessary java
sudo apt-get install openjdk-8-jre-headless -y
sudo apt-get install openjdk-8-jdk-headless -y
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
sudo apt-get update && sudo apt-get install elasticsearch
# To Configure
sudo vi /etc/elasticsearch/elasticsearch.yml
Update below fields

sudo grep -v '^$\|^\s*#' /etc/elasticsearch/elasticsearch.yml
path.data: /var/lib/elasticsearch
path.logs: /var/log/elasticsearch
network.host: 0.0.0.0 
discovery.seed_hosts: ["127.0.0.1"]
cluster.initial_master_nodes: ["node-1"]

```

# Elastic Stack

## Elasticsearch

### インストール

```console
$ sudo apt-get install apt-transport-https
$ echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
$ sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys D27D666CD88E42B4
$ sudo apt-get update && sudo apt-get install elasticsearch
$ sudo cp elaasticsearch.yml /etc/elasticsearch/elasticsearch.yml
```

### systemctlタイムアウトの調整

初期状態ではタイムアウトが75秒なので、Raspberry Piでは間に合わない。3分に伸ばす。

```console
$ sudo mkdir /etc/systemd/system/elasticsearch.service.d
$ echo -e "[Service]\nTimeoutStartSec=180" | sudo tee /etc/systemd/system/elasticsearch.service.d/startup-timeout.conf
$ sudo systemctl daemon-reload
```

## Kibana

### インストール

リポジトリ設定はElasticsearchで対応済みなので不要

```console
$ sudo apt-get install kibana
$ sudo cp kibana.yml /etc/kibana/kibana.yml
```

## 起動設定

```console
$ sudo systemctl enable elasticsearch
$ sudo systemctl enable kibana
```

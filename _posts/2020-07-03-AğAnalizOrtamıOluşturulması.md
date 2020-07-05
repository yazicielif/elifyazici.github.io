---
layout: post
title: Elastic STACK ile Ağ Analiz Ortamının Oluşturulması
bigimg: /img/network_post_1/networkimage.jpg


tags: [Network, Elastic STACK, Elasticsearch, Filebeat, Kibana]
comments: true
---


Merhabalar,
Bu yazımızda Elastic STACK üzerinde ağ analizi ortamı oluşturacağız.

Bu ortam için gereken araçlar:
- Elasticsearch
- Fiebeat
- Kibana
- Wireshark/Tshark

Ben Ubuntu 18.04 makinede çalıştığım için bu şekilde indirmekteyim.Bu kurulum Elasticsearch 7.0 ve sonrası sürümleri desteklemektedir. 

## ElasticSearch Kurulumu

sudo wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -

![](http://yazicielif.github.io/img/network_post_1/n_1.png)

sudo apt-get install apt-transport-https

![](http://yazicielif.github.io/img/network_post_1/n_2.png)

sudo echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list

![](http://yazicielif.github.io/img/network_post_1/n_3.png)

sudo apt-get update && sudo apt-get install elasticsearch

![](http://yazicielif.github.io/img/network_post_1/n_4.png)

sudo -i service elasticsearch start ile elasticsearch başlatılabilir.
netstat -nltp ile çalışan servislerde elasticsearch'ün çalıştığı 9200 portunu gözlemleyebiliriz.

![](http://yazicielif.github.io/img/network_post_1/n_5.png)


~~~
 
~~~

Bunları Elastic'in kendi sitesinde de bulabilirsiniz. Kurulumunuza bağlı olarak çalıştırma şeklinizin değişeceği için diğer yazılara referans olması açısından adım adım paylaştım. Umarım işinize yarar, sağlıcakla.


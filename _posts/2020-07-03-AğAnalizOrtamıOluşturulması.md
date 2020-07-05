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

Ben Ubuntu 18.04 makinede çalıştığım için bu şekilde indiriyorum.

sudo wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -

![](http://yazicielif.github.io/img/network_post_1/n_1.png)

sudo apt-get install apt-transport-https

![](http://yazicielif.github.io/img/network_post_1/n_2.png)

sudo echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list

![](http://yazicielif.github.io/img/network_post_1/n_3.png)

sudo apt-get update && sudo apt-get install elasticsearch


~~~
 
~~~

Bunları Elastic'in kendi sitesinde de bulabilirsiniz. Kurulumunuza bağlı olarak çalıştırma şeklinizin değişeceği için diğer yazılara referans olması açısından adım adım paylaştım. Umarım işinize yarar, sağlıcakla.


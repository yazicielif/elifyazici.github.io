---
layout: post
title: Elastic STACK ile Ağ Analiz Ortamının Kurulumu
bigimg: /img/network_post_1/networkimage.jpg


tags: [Network, Elastic STACK, Elasticsearch, Filebeat, Kibana]
comments: true
---


Merhabalar,
Bu yazımızda Elastic STACK üzerinde ağ analizi ortamı kuracağız.

Bu ortam için gereken araçlar:
- Elasticsearch
- Filebeat
- Kibana
- Tshark

Ben Ubuntu 18.04 makinede çalıştığım için bu şekilde indirmekteyim.Bu kurulum Elasticsearch 7.0 ve sonrası sürümleri desteklemektedir. 

## Elasticsearch Kurulumu


~~~
sudo wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
~~~

![](http://yazicielif.github.io/img/network_post_1/n_1.png)

~~~
sudo apt-get install apt-transport-https
~~~

![](http://yazicielif.github.io/img/network_post_1/n_2.png)

~~~
sudo echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-7.x.list
~~~

![](http://yazicielif.github.io/img/network_post_1/n_3.png)

~~~
sudo apt-get update && sudo apt-get install elasticsearch
~~~

![](http://yazicielif.github.io/img/network_post_1/n_4.png)

~~~
sudo -i service elasticsearch start
~~~

 ile elasticsearch başlatılabilir.

~~~
netstat -nltp 
~~~

ile çalışan servislerde Elasticsearch'ün çalıştığı 9200 portunu gözlemleyebiliriz.

![](http://yazicielif.github.io/img/network_post_1/n_5.png)


## Kibana Kurulumu
~~~
sudo apt-get update && sudo apt-get install kibana
~~~

![](http://yazicielif.github.io/img/network_post_1/n_6.png)

~~~
sudo -i service kibana start
~~~

localhost:5601 adresi url'e yazılır ve aşağıdaki kibana arayüzü gözlenir.

![](http://yazicielif.github.io/img/network_post_1/n_7.png)


## Tshark Kurulumu

~~~
sudo apt install tshark
~~~

Tshark kök kullanıcı modunda aşağıdaki komutla çalıştırılır.Bu komut ile packet capture işlemi ek ile Elasticsearch'ün indeksleyebileceği bir formata uygun olarak tshark.json dosyasına gerçek zamanlı olarak kaydedilir.
~~~
tshark -i 1 -T ek -V > /home/machine3/Desktop/logs/tshark.json
~~~

![](http://yazicielif.github.io/img/network_post_1/n_10.png)


## Filebeat Kurulumu

~~~
sudo apt install filebeat -f
~~~

![](http://yazicielif.github.io/img/network_post_1/n_8.png)

Filebeat etc dizini altına gidilir.

![](http://yazicielif.github.io/img/network_post_1/n_9.png)


 Buradaki filebeat.yml dosyası aşağıdaki gibi düzenlenir. Aşağıdaki konfigürasyon için “Filebeat 7.6 Klavuzu”ndan faydalanılmıştır.

~~~
filebeat.inputs:
- type: log
  enabled: true
  paths:
    - /home/machine3/Desktop/logs/tshark.json
  json.keys_under_root: true
  fields:
   document_type: "pcap_file"


filebeat.config.modules:
  
  path: ${path.config}/modules.d/*.yml

  reload.enabled: false

setup.template.settings:
  index.number_of_shards: 1

setup.kibana:
  host: "localhost:5601"

output.elasticsearch:
  
  hosts: ["localhost:9200"]
  

processors:
 - drop_event:
     when:
       equals:
         index._type: "pcap_file"
~~~

▪ İnput bölümünde ;
- input olarak gelen verinin log tipinde olacağı,
- paths kısmında geldiği dizini,
- json.key_under_root: true ile varsayılan olarak, kodu çözülen JSON çıktı belgesindeki bir "json" anahtarının altına yerleştirilir. Bu ayarı etkinleştirilerek anahtar çıktı belgesinde en üst seviyeye kopyalanır. Varsayılan, false değeridir.
- Document_type : “pcap_file” ile gelen dosyanın pcap dosyası türünde olduğunu belirtildi.


▪ Setup.kibana : host : “localhost5601” Kibana ‘nın hostunu konfigüre edildi.

▪ Output.elasticsearch: host: [“localhost:9200”] ile Elasticsearch ‘ ün output’unu konfigüre edildi.

▪ processors: - drop_event: when: equals: index._type: "pcap_file" ile indeks tipi “pcap_file” olan dosyaların drop (düşme) işlemi gerçekleştirildi.



~~~
sudo systemctl start filebeat 
~~~

~~~
sudo systemctl status filebeat 
~~~

![](http://yazicielif.github.io/img/network_post_1/n_11.png)


Kibana'ya gelinir. Management kısmından Create index pattern ile indeks paterni oluşturulur. Index Management kısmında patternlere gelen yeni veriler reload indices ile yenilenebilir. 


![](http://yazicielif.github.io/img/network_post_1/n_12.png)

Kibana Dashboard kısmına gelerek görselleştirilme yardımıyla paketler incelenebilir.


![](http://yazicielif.github.io/img/network_post_1/n_13.png)
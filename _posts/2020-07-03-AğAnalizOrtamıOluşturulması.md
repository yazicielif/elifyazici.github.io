---
layout: post
title: Elastic STACK ile Ağ Analiz Ortamının Oluşturulması
bigimg: /img/network_post_1/networkimage.jpg


tags: [Docker, Dockerfile]
comments: true
---


Merhabalar,
Bu yazımızda en basit haliyle python derleyebileceğimiz bir Docker Image oluşturmaktan bahsedeceğiz.

Docker dosyasını oluşturacağımız dizini oluşturup cd ile içine giriyoruz. Ardından Dockerfile adında bir dosya oluşturup nano ile düzenlemek için gereken komutu giriyoruz.

![](http://yazicielif.github.io/img/docker_post/docker_post_1.png)

Açılan DockerImage'in içine aşağıdaki komutları yazıyoruz.

~~~
FROM ubuntu:16.04

RUN apt update && apt -y install python

COPY *.py / 
~~~

Bu komutlarda;
- **FROM** Base Image belirtmek için kullanılan komuttur.
- **RUN**  Image oluşturulurken çalıştırılması istenin linux komutları buraya yazılır.
- **COPY** Host makinedeki belirtilen dosya ve klasörleri Container içine kopyalamak için kullanılır.

![](http://yazicielif.github.io/img/docker_post/docker_post_2.png)

hello.py adında bir python dosyası oluşturup içine basit olması açısından hello world yazdırıyoruz. Image içinde sadece Dockerfile ve python dosyası bulunuyor. 

![](http://yazicielif.github.io/img/docker_post/docker_post_3.png)

sudo docker build . komutu ile bulunduğumuz dizindeki dosyalardan Docker Image oluşturuyoruz. 

![](http://yazicielif.github.io/img/docker_post/docker_post_4.png)

sudo docker images ile tüm image leri listeleyebiliyoruz.

![](http://yazicielif.github.io/img/docker_post/docker_post_5.png)

Yukarda da görüldüğü gibi etiketlendirilmemiş bir image imiz bulunuyor. Bu image e sudo docker tag <<Image ID>>  <<containeradı>> etiket veriyoruz.

![](http://yazicielif.github.io/img/docker_post/docker_post_6.png)

sudo docker run -d -it --name <<dockeradı>> <<containeradı>> komutu ile  docker a isim vererek Container çalıştırılır. 

![](http://yazicielif.github.io/img/docker_post/docker_post_7.png)

Çalışan Container ları görüntülemek için sudo docker ps komutu girilir.

![](http://yazicielif.github.io/img/docker_post/docker_post_8.png)

sudo docker exec -it <<dockeradı>> bash ile docker ımız bir bash e çıkartılır. ls ile içini görüntülediğimiz docker da kopyaladığımız python dosyasını görmekteyiz. Dockerfile dosyası içine RUN ile python kurulumunu da gerçekleştirdiğimizden dolayı içerde python derlemek için python hello.py dememiz yeterli.

![](http://yazicielif.github.io/img/docker_post/docker_post_9.png)



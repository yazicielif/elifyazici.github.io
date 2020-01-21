---
layout: post
title: Could not resolve host hatası çözümü
#subtitle: 
comments: true
---

Arkadaşlar merhaba yaşadığım bir sıkıntı ve çözümü için bu yazıyı hazırladım.
Fiziksel sistemime sorunsuz bir şekilde ubuntu kurulumu ve güncellemeler yaptım fakat ihtiyacım olan programları kurmaya başladığımda aşağıdaki gibi
~~~
Hata:  1 https://download.docker.com/linux/ubuntu xenial InRelease             
  Could not resolve host:
~~~
hatası aldım konu ile ilgili birçok araştırma yaptım.
Problemi çözemedim ve sorunsuz bir internetim olduğu halde  başka bir ağdan internete bağlanmayı denedim ve hatam çözüldü.
Kullandığım ağ public di ve authentication ile internete giriş yapılıyordu ancak internete giriş portalının ssl sertifikası olmaması bu sorunları yaşamama sebep olmuştu.

![Crepe](https://hizliresim.com/anVLpB)

Çözüm olarak cat /etc/resolv.conf dosyasına giderek içerisine google dns ayarlarını yazabilirsiniz.

~~~
nameserver 8.8.8.8
nameserver 8.8.4.4
~~~

Konu ile ilgili detaylı bilgi için
man apt-secure den bilgi alabilirsiniz.
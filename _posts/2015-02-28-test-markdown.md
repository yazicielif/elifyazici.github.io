---
layout: post
title: Could not resolve host hatası çözümü
#subtitle: 
comments: true
---


Fiziksel sistemime sorunsuz bir şekilde ubuntu kurulumu ve güncellemeler yaptım fakat ihtiyacım olan programları kurmaya başladığımda aşağıdaki gibi
~~~
Hata:  1 https://download.docker.com/linux/ubuntu xenial InRelease             
  Could not resolve host:
~~~
hatası aldım konu ile ilgili birçok araştırma yaptım.
Problemi çözemedim ve sorunsuz bir internetim olduğu halde  başka bir ağdan internete bağlanmayı denedim ve hatam çözüldü.
Kullandığım ağ public di ve authentication ile internete giriş yapılıyordu ancak internete giriş portalının ssl sertifikası olmaması bu sorunları yaşamama sebep olmuştu.

~~~
~$ sudo apt-get update
Hata:  1 https://download.docker.com/linux/ubuntu xenial InRelease             
  Could not resolve host: download.docker.com
Yoksay:2 http://dl.google.com/linux/chrome/deb stable InRelease                
Aynı:  3 http://dl.google.com/linux/chrome/deb stable Release                  
Aynı:  5 http://tr.archive.ubuntu.com/ubuntu xenial InRelease                  
İndir: 6 http://tr.archive.ubuntu.com/ubuntu xenial-updates InRelease [109 kB]
İndir: 7 http://tr.archive.ubuntu.com/ubuntu xenial-backports InRelease [107 kB]
İndir: 8 http://tr.archive.ubuntu.com/ubuntu xenial-security InRelease [109 kB]
İndir: 9 http://tr.archive.ubuntu.com/ubuntu xenial-updates/main amd64 Packages [995 kB]
İndir: 10 http://tr.archive.ubuntu.com/ubuntu xenial-updates/main i386 Packages [843 kB]
İndir: 11 http://tr.archive.ubuntu.com/ubuntu xenial-updates/main amd64 DEP-11 Metadata [323 kB]
İndir: 12 http://tr.archive.ubuntu.com/ubuntu xenial-updates/main DEP-11 64x64 Icons [233 kB]
İndir: 13 http://tr.archive.ubuntu.com/ubuntu xenial-updates/universe amd64 DEP-11 Metadata [274 kB]
İndir: 14 http://tr.archive.ubuntu.com/ubuntu xenial-updates/universe DEP-11 64x64 Icons [400 kB]
İndir: 15 http://tr.archive.ubuntu.com/ubuntu xenial-updates/multiverse amd64 DEP-11 Metadata [5.968 B]
İndir: 16 http://tr.archive.ubuntu.com/ubuntu xenial-updates/multiverse DEP-11 64x64 Icons [14,3 kB]
İndir: 17 http://tr.archive.ubuntu.com/ubuntu xenial-backports/main amd64 DEP-11 Metadata [3.328 B]
İndir: 18 http://tr.archive.ubuntu.com/ubuntu xenial-backports/universe amd64 DEP-11 Metadata [5.104 B]
İndir: 19 http://tr.archive.ubuntu.com/ubuntu xenial-security/main amd64 DEP-11 Metadata [73,8 kB]
İndir: 20 http://tr.archive.ubuntu.com/ubuntu xenial-security/main DEP-11 64x64 Icons [73,2 kB]
İndir: 21 http://tr.archive.ubuntu.com/ubuntu xenial-security/universe amd64 DEP-11 Metadata [124 kB]
İndir: 22 http://tr.archive.ubuntu.com/ubuntu xenial-security/universe DEP-11 64x64 Icons [188 kB]
İndir: 23 http://tr.archive.ubuntu.com/ubuntu xenial-security/multiverse amd64 DEP-11 Metadata [2.464 B]
Hata:  24 http://linux.teamviewer.com/deb stable InRelease                     
  'linux.teamviewer.com' çözümlenirken geçici bir sorunla karşılaşıldı
Hata:  25 http://packages.osrfoundation.org/gazebo/ubuntu-stable xenial InRelease
  'packages.osrfoundation.org' çözümlenirken geçici bir sorunla karşılaşıldı
60 sn.'de 3.882 kB alındı (64,6 kB/s)           
Paket listeleri okunuyor... Bitti
W: https://download.docker.com/linux/ubuntu/dists/xenial/InRelease alınamadı Could not resolve host: download.docker.com
W: http://packages.osrfoundation.org/gazebo/ubuntu-stable/dists/xenial/InRelease alınamadı 'packages.osrfoundation.org' çözümlenirken geçici bir sorunla karşılaşıldı
W: http://linux.teamviewer.com/deb/dists/stable/InRelease alınamadı 'linux.teamviewer.com' çözümlenirken geçici bir sorunla karşılaşıldı
W: Bazı indeks dosyaları indirilemedi. Bu dosyalar yok sayıldılar ya da önceki sürümleri kullanıldı.
~~~

Çözüm olarak cat /etc/resolv.conf dosyasına giderek içerisine google dns ayarlarını yazabilirsiniz.

~~~
nameserver 8.8.8.8
nameserver 8.8.4.4
~~~

Konu ile ilgili detaylı bilgi için
man apt-secure den bilgi alabilirsiniz.
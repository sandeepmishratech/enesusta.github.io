---
title: Docker nedir? 
tags: [go, docker]
style: fill
color: info
description: Docker hakkında.
#external_url: https://blog.usejournal.com/how-to-undo-your-git-failure-b76e31ecac74
---



#### Sanallaştırma

Sanallaştırma yazılım endüstrisinin en sevdiği şey. Yazılıma hizmet eden herşeyi sanallaştırabiliyoruz.

Sanallaştırmayı maddelere ayırmak gerekirse;

- CPU
- Bellek
- Sabit disk
- Ağ arayüzü
- USB
- 
Günümüz itibari ile artık **VMWare, Hyper-V** gibi teknolojileri kanıksadık. Fiziki bir donanım üzerinde **sanal donanımlar** `varmış` gibi çalışıyor ve aşılması güç sorunları bu vesile ile aşılır kılıyoruz.

Sanallaştırıyoruz çünkü;

- Anlaşılmaz donanım problemleriniz azaltıyoruz.
- Yedekleme işlerini kolaylaştırıyoruz.
- Birbirinden bağımsız olması gereken (izolasyon) kaynakları ayrıştırıyoruz.

Neden bağımsız işletim sistemi ve onların sanal donanımlarına ihtiyaç duyuyoruz? Evet, oraya koyacağımız uygulamalar özelinde daha ciddi kaynak yönetimi ve izolasyon için.

Bir diğer kullanım amacı nedir? Orkestrasyon yani birden fazla sanal sunucu veya container'in birbiri ile paralel ve senkronize bir şekilde çalışması. 

Orkestrasyon işini docker tarafında halleden belli başlı araçlar:

- Kubernetes
- Docker Swarm
- Openshift
- Google Container Engine
- AWS EKS Service

Bu bilgiler ışığında **sanallaştırma ile ilgili olarak** sorun nedir?


En temel sorun; **gereksiz** kaynak tüketimi.

Şu şekilde örneklemek gerekirse, bir **host os** üzerinde **100mb** tüketime sahip bir uygulamayıda **host** edecek olsak o işletim sisteminin içine (sanal makineye) koymak gerekiyor.

Dolayısı ile yanlızca 100 mb'lık bir uygulama için;

- Devasa boyutlarda işletim sistemini ayağa kaldırmak gerekiyor.
  - Ubuntunun kurulumu için ihtiyaç duyduğu alan **4.5GB**.
  - Windows 10 ise **32 GB** alana ihtiyaç duyuyor.
- Devasa bir **OS'i** kaldırmak yetmiyor, uygulamamızıda bu işletim sistemi içerisine koymamız gerekiyor.

Bu da esasında uygulama için ayırmış olduğumuz kaynağın aslında bir kısmının (**oldukça büyük bir kısmının**) **gereksiz** yere işletim sistemi tarafından kullanılması anlamına geliyordu.

Bununlada bitmiyor. 

Bir VM'i ayağa kaldırmak **en az** 2-3 dakikadan 10-15 dakikaya kadar sürüyor. 

Firmalar bakıyor ki bu iş bu şekilde ilerlemez. Bu durum hem hosting firmasına, hem müşteriye zarar çünkü;
-  müşteri parasının hakkını tam olarak alamıyorken (vm kaynaklı **gereksiz** kaynak tüketimi sebebi ile)
-  hosting firmasıda daha çok hdd kullanımı yüzünden (en basit OS min 5GB) daha fazla VM ayağa kaldıramıyordu.

Bu durumu farkeden **Google** ve **Linux**'tan birkaç geliştirici linux **kernel**ında bir değişikliğe gidiyorlar ve kernel'a;

- **cgroups**
- **namespace**

adı altında iki yeni **yapı** ekliyorlar. Bu yapılar ile birlikte artık linux dünyasına **container** diye bir kavram girmiş oluyor.

##### Container nedir?

OS üzerinde prosesler(işlemler) birbiirnden bağımsız olarak yönetilir. Fakat **container** mantığı bu izolasyonu daha ileri götürüyor.

Bir prosese sanal (yavru) bir işletim sistemi sunuyor. Kernel seviyesinde gerçekleşen bu işlem sonucunda proses kendini tek başına çalışan bir işletim sistemi ortamında **zannediyor**.

Yani VM'lerin aksine;

```bash
VMler işletim sistemi ile uygulamalar arasına katman ekliyorken, Docker bu aradaki katmanı kaldırıyor.
```

Container kavramı çok yeni bir kavramda değil, ilk örneği UNIX (**hala bilmeyenler için dünyanın ilk işletim sistemi olur kendisi**) dünyasında **chroot** ile 80'lerde başlıyor. 
Yukarıdada bahsedildiği üzere **Google** tarafından 2006'da geliştirilmeye başlanan ve 2008 yılındada resmen Linux çekirdeğine eklenen **control groups(cgroups)** özelliği ile olgunlaşıyor.

Cgroups proseslerin kaynak kullanımlarını sınırlamayı sağlıyor ve güçlü yalıtım getiriyor.

Kernel imkanlarını sununca bağımsız container implementasyonları doğmayı başlıyor.

Bu implementasyonlardan bir diğeri;

- LXC (Linux containers'ın kısaltılması)

Docker ortaya çıktığı ilk zamanlarda var olan container konseptinin üzerine kurulmuş bir uygulama dağıtım aracı olarak ortaya çıkıyor.

Mayıs 2013 yılında bir **Python** konferasında Docker'in geliştiricisi olan **Solomon Hykes** tarafından tanıtılıyor.

{% include elements/video.html id="wW9CAH9nSLs" %}













{% include elements/figure.html image="https://raw.githubusercontent.com/enesusta/assets-host-for-github-pages/master/docker-nedir/docker-nedir1.png" caption="The Ocean" %}
{% include elements/figure.html image="https://raw.githubusercontent.com/enesusta/assets-host-for-github-pages/master/docker-nedir/docker-nedir2.png" caption="The Ocean" %}












































































































































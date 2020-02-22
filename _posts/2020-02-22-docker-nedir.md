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

**Hypervisor**’lerle kurulan bir sanallaştırma altyapısında **yeni bir node’un** (sanal makina) sisteme eklenmesi için öncelikle işletim sisteminin **hypervisor üzerinde boot edilerek** başlatılmasının beklenmesi gerekmektedir.


İşletim sisteminin başlatılması için ise ;
- ön yükleyicinin (boot loader) işletim sistemini belleğe yüklemesi,
- sanallaştırılan donanım bileşenlerinin (sanal disk, sanal ekran kartı, vb) kullanıma hazır hale getirilmesi ile
- işletim sistemi modüllerinin kullanıma hazır hale getirilmesinin beklenmesi gereklidir. 

Yukarıda listelenen sebeplerden dolayı bir VM'i ayağa kaldırmak **en az** **2-3** dakikadan **10-15 dakikaya kadar** sürüyor. 

Docker tarafında ise;

- Bütün bu işlemler en iyi ihtimalle **20-25 saniye** sürmektedir.
- `Docker ile yeni bir node (Container)` eklenmesi ise **milisaniyeler mertebesinde (50 - 100 ms)** gerçekleştirilebilmektedir.

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

LXC cgroup ile yönetilmesi zor olan container'ların daha kolay yönetilmesini sağlayan bir araçtır.

Docker ortaya çıktığı ilk zamanlarda var olan container konseptinin üzerine kurulmuş bir uygulama dağıtım aracı olarak ortaya çıkıyor.

Mayıs 2013 yılında bir **Python** konferasında Docker'in geliştiricisi olan **Solomon Hykes** tarafından tanıtılıyor.

{% include elements/video.html id="wW9CAH9nSLs" %}


Docker'in tanıtılması ile **eski ve hantal** VM'ler ve onların içerisinde ayrı işletim sistemleri ve onlarında içinde ( **inception** ) uygulamaları koşmak yerine direk **host os** üzerinde **container'lar** içerisinde uygulamalar koşuyor.

Yani;

- Container'lar doğrudan host os'in kaynaklarını kullanıyor ve kendi içlerinde bir **işletim sistemi barındırmıyor.**
- Bu da; 100 mb'lik bir uygulamayı **container** ile ayağa kaldırdığımız zaman sadece 100mb'lık bir alan kapsıyor ve aynı zamanda **işletim sistemi vs barındırmadığı için** ilgili container için belirlenen kaynaklar tam anlamı ile **uygulama tarafından** kullanılabilir anlamına geliyor.


##### Docker'in çözmeye aday olduğu problemler

1.  Docker **ama benim makinemde çalışıyor** serzenişini çözer.
    - Geliştirme ortamı ile production(ürün) ortamı farklılıklar gösterir. Dolayısı ile geliştirme ortamında çalışan bir uygulama production ortamında çalışmayabilir.
    - Docker ile birlikte uygulamalarımızı Docker altyapısı ile **paketlediğimiz için** aynı **Image**ı 
      - hem Geliştirici ortamında
      - hem UAT (**User Acceptance Test - Kullanıcı Kabul Testi**) ortamında
      - ve Production ortamında kullanabiliriz.
    - DEV ve UAT ortamlarında tek bir Container'ın çalıştırılması yeterli olacakken **PROD ortamında gerektiği kadar Container ayağa kaldırılarak `Bir load balancer(yük dengeleyici) yardımıyla dağıtılabilir`**
2.  Geliştirme ortamı standardizasyonu sağlaması
    - Bazı yazılım evleri, farklı müşterilerde farklı sürümleri bulunan kurulumları geliştirici ortamlarında tekrarlayabilmek için geliştirici ortamlarını sanal sunucularda tutmaktadır. Bir sanal makinenin **ortalama 20GB** olduğu düşünülürse tek bir projenin 5 müşteride kurulu olması halinde her bir geliştiricinin bilgisayarında **100GB'lık** bir alan gerekli olacaktır.
    - Her yapısal değişiklikte
      - Web sunucu değişimi
      - Database şeması veya referans data değişikliği
    - binary formatta olan **master vm'in** bütün geliştiricilere dağıtılması ve varsa geliştiricilerin kendi özelleştirmeleirni bu makinalara tekrar uygulamak zorunda olması gibi **angarya işler** den kurtarır.

#### Docker vs VM's

{% include elements/figure.html image="https://raw.githubusercontent.com/enesusta/assets-host-for-github-pages/assets/docker-nedir/docker-nedir4.png" caption="Infrastructure of VM's" %}

{% include elements/figure.html image="https://raw.githubusercontent.com/enesusta/assets-host-for-github-pages/assets/docker-nedir/docker-nedir5.png" caption="Infrastructure of Docker" %}

Docker **VM**lerin aksine tek bir işletim sistemi üzerinde birden çok prosesi **bağımsız** olarak çalıştırır.

Bugün itibari ile **VMWare'in** en büyük rakibi şuanda ne **hyper-v** ne de **kvm'dir.** 

En büyük rakibi artık **Docker.** 

Çünkü Docker ve beraberinde güçlenen container altyapısı, **donanım sanallaştırmasına** ciddi bir cephe açmış durumda. Herkes birbirinin **tamamlayıcısı** diye **yumuşak** yorumlar yapıyor olsalar da **VMWare** gibi yerlerde Docker **soğuk rüzgarlar** estiriyor.

Daha önceleri **VMWare** imageları ile dağıtılan yazılımlar şimdi Docker image'ları ile dağıtılıyor.

Kullanması da iki üç komuta bakıyor;

- `docker-compose up` gibi.

Artı olarak sıradan bir proses olark çalışıyor.

Çeviklik (agile) istediğimiz **microservislerin hüküm sürdüğü** bir çağda

- **Infrastructure as Code**
- **Immutable Infrastructure**
- **Disposable Server** gibi kavramları konuştuğumuz bir çağda;

Sanallaştırma çözümleri **prangalarından** dolayı arzu edilen çevikliğe **asla** ulaşamayacaklar.

Dolayısı ilede **sanallaştırma** artık **legacy(eskimiş, modası geçmiş, miras)** bir çözüm olmuştur. **Containerization** çözümü yeni nesil sanallaştırma çözümüdür.

Bu noktada **Microsoft** için olumlu bir not eklenebilir; Olayın gidişatını erkenden kavrayıp **Hyper-V'yi** container uyumlu hale getirdi. Yarına **bugünden hazırlanan** bir Microsoft.

Yarın, insanlar sanal işletim sistemlerini konuşmayacaklar artık.

- Tek bir işletim sistemi
- Tek bir kernel

Ve üzerinde yeterince izole olmuş her biri kendini **husisi bir işletim sisteminde zanneden prosesler** açılıp kapanmaları iş değil. Sürüm geçmek saniye sürüyor. Yeni prosesi aç, eskisini kapat.

Ve tüm bunlar bir kaynak kod deposu ile **uçtan uca bağlı**.

### Gerçek dünyada nasıl kullanıyoruz?

Varsayalım ki ufak ölçekli bir yazılım firmasıyız ve elimizde çok kaynakta yok.

3 Farklı şirkete **A, B, C** için web sitelerini internette yayınlayacağız ve para alacağız.

1 GB'lık bir **statik IP** sahibi bir cihazımız olsun. Değil **3 adet** bir tane bile **VM** kuramıyoruz. (RAM yetmiyor)

Yine bir Docker çözümü olan **docker-compose** aracı ile birden fazla container'i rahatlıkla yönetebiliyoruz.

Bunun için şu şekilde bir dosyaya sahip olacağız;

```yml
version: '2'

services:
    company_a_web_server:
        image: nginx:latest
        ports: 
            - "8001:80"
    
    company_b_web_server:
        image: nginx:latest
        ports:
            - "8002:80"
    
    company_c_web_server:
        image: nginx:latest
        ports:
            - "8003:80"
```

**NGINX** bir web sunucusu olduğu için default olarak **80 HTTP** portunu dinliyor. 

**ports** kısmında verdiğimiz;

- ilk argüman **host os** üzerinden erişmeye çalışacağımız **port numaramız**.
- ikinci argüman ise **container** içerisinde çalışan uygulamanın **portu**

**Tek bir komut** ile 3 adet şirket için 3 adet **NGINX** uygulaması ayağa kaldırdık.

{% include elements/figure.html image="https://raw.githubusercontent.com/enesusta/assets-host-for-github-pages/assets/docker-nedir/docker-nedir6.gif" caption="Uygulamamızın uygulanışı" %}

Gördüğünüz üzere sadece **5.49 saniye** içerisinde 3 farklı **NGINX** container'i ayağa kalktı.

Peki bu container'lar toplamda ne kadar **kaynak** tüketiyor?

{% include elements/figure.html image="https://raw.githubusercontent.com/enesusta/assets-host-for-github-pages/assets/docker-nedir/docker-nedir7.png" caption="Docker stats" %}


Evet **yanlış görmüyorsunuz** toplamda sadece **4.5 MB** kullanılıyor.

























































































































---
title: Git nedir?
tags: [git, unix]
style: fill
color: primary
description: 28 Şubat 2020 tarihli Git Nedir? eğitimine ilişkin sunum notları.
comments: true
#external_url: https://blog.usejournal.com/how-to-undo-your-git-failure-b76e31ecac74
---

#### Versiyon nedir?

İnsanoğlu yazıyı keşfetmeden önce dahi mağara duvarlarına resimler yaparak düşüncelerini somutlaşma eğiliminde olagelmişlerdir. Bilinen tarihe göre ilk yazı **Sümerliler** tarafından **İsa'dan önce 3500 civarlarında icat edildi.**  


O günün insanları bu yol / yollar ile ilk dökümanları oluşturmuş ve bu dökümanları iletişim aracı olarak kullanmışlardır.

Bizler ise bugün şunu yapıyoruz;

Latin alfabesinde yer alan karakterleri kullanarak bilgisayarda dijital dökümanlar oluşturuyoruz, arkadaşlarımızla sohpet ediyoruz yada derste not çıkarıyoruz.

Bunun sonucundada dijital yahut değil, **bir döküman oluşuyor.**

Her döküman oluştuğu ilk saniyeden itibaren bir **versiyon ihtiva eder**. Basit bir silgi darbesi dahi vursanız artık o döküman aynı döküman değildir ve zaman içinde bu gibi **değişiklerin** her birine **versiyon** diyoruz.

Deftere;

İlk sene;
- Dünyanın en güzel okulunda okumuyorum **sanırım**. 
  - yazdık, bu defter adlı ürünün **0.0.1** versiyonu;

İkinci sene;

- Dünyanın en güzel mühendislik fakültesinde okumuyorum **sanırım**.
  - yazdık, artık bu değişiklik ile birlikte **0.0.2** versiyona geçtik;

Üçüncü sene;

- Dünyanın en kötü okulunda okuyorum.
  - yazdık, artık defter **0.0.3** versiyonunda;

Son sene;

- Dünyanın en kötü mühendislik fakültesinde okuyorum.
  - yazdık, artık defter **0.0.4** versiyonunda;


4 yıllık bir zaman dilimine dair versiyonlamanın işleyişini bu kadar basit bir şekilde özetleyebiliyoruz.



#### Versiyonlamanın dertlerini nasıl aştık?

Önce tanım;

##### Nedir bu dertler?

Varsayalım ki burada bulunan 30 kişi (**yazar burada 30 kişiye bu sunumu yapıyor olduğunu varsaymaktadır**) ile **birlikte** bir proje geliştiriyoruz.

- Hangi değişiklikler yapıldı?
- Değişiklikleri kim yaptı?
- Değişiklikler ne zaman yapıldı?
- Neden değişikliğe ihtiyaç duyuldu?





Sıralanmış bulunan dertleri VSC (**Version Control System**) adını vermiş olduğumuz sistemler aracılığı ile çözebildik.

Bir sürüm kontrol sistemi vasıtası ile insanlar ve ekipler proje / projeler üzerinde birlikte çalışabilme fırsatı yakalıyor. 



Bugün 2020 yılında yaşayan insanlar olarak ne gibi VCS'leri kullanabiliriz?

- SVN
- Git
- Mercurial
- Bazaar

#### Neden versiyon kontrolüne ihtiyacımız var?

##### Uyumlu ekip çalışması

Herhangi bir versiyon kontorl sistemi kullanmayacak kadar kendimize güveniyorsak, beraber çalıştığımız diğer kişiler ile aynı dosyalar üzerindne çalışabilmek için muhtemelen herkesin erişimine açık **paylaşımlı** bir klasör kullanmak durumunda kalacağız.

Bu tür bir çalışma hem çok zahmetli hem de hatalara açıktır.

Örneğin;

- Bir dosyanın en son geçerli versiyonunun nerede olduğunun takip edilmesi gibi çözüm bulunması gereken sorunlar ile uğraşmak zorunda kalacağız.
  - Üzerinde çalıştığımız dosyada bizden önce başkasının **değişiklik** yapıp yapmadığından haberimiz yoksa **hatalı** içerik üretme ihtimalimiz artacaktır.

Versiyon kontrol sistemi kullanma yoluna gidersek;

- Ekibimizdeki herkes özgür bir şekilde istediği dosyalar üzerinde güvenli bir şekilde istediği değişikliği yapabilir. Herkes değişikliklerini tamamladıktan sonra da **tüm değişiklikler** versiyon kontrol sistemi kullanılarak sağlıklı bir şekilde **merge(birleştirme)** edilebilir.

---

#####  Versiyonların düzgün bir şekilde takip edilebilmesi

{% include elements/figure.html image="https://i.pinimg.com/originals/07/c6/dc/07c6dc9f7d0439ae7c2e2866cc975af4.jpg" caption="Neden VCS kullanmalısınız?" %}


##### Önceki Versiyonlara Geri Dönebilme

Zira Türkay'ın yahut Onur'un yaptığı geliştirmeyi (**değişikliği**) an be an görüntüleyebilirim, onlarda yapmış olduğum yahut yapacağım **değişiklikleri** görüntüleyebilirler.

Veya; 

- Onurun sebep olduğu / olacağı hatalı bir kod sebebiyle işlev dışı olan bir projenin çalışan **sağlam** haline geri dönüş yapabiliyoruz.

Version Control System'leri bize bunu sunuyor diyebiliriz.

##### Yedekleme

Git gibi dağıtık versiyon kontrol (DVCS) sistemlerinin yan etki olarak sağladığı faydalardan birisi de yedeklemedir. 

#### Git'e giriş

Git 2005 yılında **Linux Torvalds** ve Linux Kernel'ini de kodlayan ekip tarafından **Linux** kaynak kodunu versiyon kontrolü altında tutmak ve kendi iş akışlarını düzenlemek için geliştirilmiştir.

Öncesinde ne vardı?

- Linux'un kaynak kodları **1991-2002** yılları arasındaki dönemde manuel olarak dosyaların paylaşılması şekilde yönetiliyordu.
- 2002 Sonrasında Open Source projeler için ücretsiz lisanslama modeli sunan **BitKeeper** isimli bir dağıtık VCS ile çalışmaya başladılar.
- 2005 yılında BitKeeper ücretsiz lisansları geri çekti ve Linux ekibi **Git'i** geliştirmek durumunda kaldı.

15 senedir de gelişmeye devam ediyor.

##### Git Konfigürasyonu

En önemli ayarımız kullanıcı adımız ve email adresimizi içeren ayardır.

Git, ayar olarak tanımladığımız değerleri **commit** vb işlerde otomatik olarak kullanır. 

Şunu yapacağız;

```git
git config --global user.name "Enes Usta"
git config --global user.email "enesusta@email.com"
```

- **--global** seçeneği ile Git'e global ayarları düzenlediğinizi söylüyoruz

Git **config** adında bir araç / komut'a sahibiz.

Git ayarlarımız aşağıda belirtilen 3 konumda kaydediliyor ve hiyerarşiş olarak bu konumlardan yüklenmekteler.

1. Seviye (/etc/gitconfig dosyası) : Tüm kullanıcı ve projeler için geçerli olan ayarlar bu dosyada kaydedilir. **git config** komutunu **--system** seçeneği ile çalıştırırsanız ayarlar bu dosyada kaydedilecek ve bu dosyadan okunacaktır
2. Seviye (/.gitconfig dosyası) : Sadece sizin kullanıcınız için tanımlanan ayarların kaydedildiği dosyadır. git **config** komutunu **--global** seçeneği ile çalıştırısanız ayarlar bu dosyaya kaydedilecek ve bu dosyadan okunacaktır
3. Seviye : Proje klasörünüzün (projenizin Git ile versiyon kontrolüne alınmış olması gerekiyor) altında yer alan **.git/config** dosyasında ise proje bazındaki git ayarlarınız yer alır.


Git, ayarlarınızın değerini belirlemek için bu üç konumdaki dosyaları 3. seviye, 2. seviye ve 1. seviye sıralaması ile **hiyerarşik olarak** okur. Belirli bir ayar'a ilişkin değere ilk hangi seviyede rastlandıysa o seviyedeki değer dikkate alınır diğer seviyelerdeki değerler dikkate alınmaz.

Global seviyede tüm ayarları listelemek için

```bash
git config --global -l
```

Global seviyede tek bir ayar'ın değerini (örneğimizde user.name anahtarına sahip ayar) görmek için ise

```bash
git config --global user.name
```

##### Editor ayarı
```bash
git config --global core.editor "code --wait"
```














































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

Zira Türkay'ın yahut Onur'un yaptığı geliştirmeyi (**değişikliği**) an be an görüntüleyebilirim, onlarda yapmış olduğum yahut yapacağım **değişiklikleri** görüntüleyebilirler.

Veya; 

- Onurun sebep olduğu / olacağı hatalı bir kod sebebiyle işlev dışı olan bir projenin çalışan **sağlam** haline geri dönüş yapabiliyoruz.

Version Control System'leri bize bunu sunuyor diyebiliriz.

Bugün 2020 yılında yaşayan insanlar olarak ne gibi VCS'leri kullanabiliriz?

- SVN
- Git
- Mercurial
- Bazaar

#### Neden versiyon kontrolüne ihtiyacımız var?

1. Uyumlu ekip çalışması

Herhangi bir versiyon kontorl sistemi kullanmayacak kadar kendimize güveniyorsak, beraber çalıştığımız diğer kişiler ile aynı dosyalar üzerindne çalışabilmek için muhtemelen herkesin erişimine açık **paylaşımlı** bir klasör kullanmak durumunda kalacağız.

Bu tür bir çalışma hem çok zahmetli hem de hatalara açıktır.

Örneğin;

- Bir dosyanın en son geçerli versiyonunun nerede olduğunun takip edilmesi gibi çözüm bulunması gereken sorunlar ile uğraşmak zorunda kalacağız.
  - Üzerinde çalıştığımız dosyada bizden önce başkasının **değişiklik** yapıp yapmadığından haberimiz yoksa **hatalı** içerik üretme ihtimalimiz artacaktır.

Versiyon kontrol sistemi kullanma yoluna gidersek;

- Ekibimizdeki herkes özgür bir şekilde istediği dosyalar üzerinde güvenli bir şekilde istediği değişikliği yapabilir. Herkes değişikliklerini tamamladıktan sonra da **tüm değişiklikler** versiyon kontrol sistemi kullanılarak sağlıklı bir şekilde **merge(birleştirme)** edilebilir.













































































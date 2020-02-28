---
title: Git nedir?
tags: [git, unix]
style: fill
color: primary
description: 28 Şubat 2020 tarihli Git Nedir? eğitimine ilişkin sunum notları.
comments: true
#external_url: https://blog.usejournal.com/how-to-undo-your-git-failure-b76e31ecac74
---

Bu yazı ve notlar **28 Şubat 2020** tarihinde Trakya Üniversitesi Bilgisayar Mühendisliği **Software Craftsmanship** topluluğu tarafından daha nitelikli mühendisler olabilmek gayesi güden öğrenciler tarafından düzenlenmiş ve gerçekleştirilmiştir.


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


### Git Kontrol Akışı

VCS'in en temel bileşeni **repository** ismini verdiğimiz yapıdır.

Repository
- dosyalarınızdaki tüm değişiklikleri
- bu değişiklikler ile ilgili ilave bilgileri 
  - değişikliği kim
  -  ne zaman yaptı 
  -  değişiklik ile ilgili girilen açıklamalar)

ayrı birer versiyon olarak kayıt altında tutan bir veri tabanıdır.

Git tüm bu bilgileri genellikle dosya sisteminde gizli bir klasör olarak oluşturulan **.git** isimli klasör içinde bir dizi dosya olarak tutar.

#### Nasıl Repository Oluşturacağım?

İki yolu var;

- `git init` komutunu kullanmak.
- `git clone` ile **git sunucusundaki** projeyi bilgisayarımıza indirmek.


Daha sonrasında;

Varsayalım ki, yapmış olduğumuz değişiklikler istediğimiz noktaya ulaştı yahut tamamlandı. Bu noktada **değişikliklerimizi** `commit` adı verilen bir bütün olarak tarif etmeliyiz.

Böylece projemizin yeni bir versiyonunu oluşturma işleminin ilk adımını tamamlamış olacağız.

#### Commit'ten önce

Yapmış olduğumuz değişikliklerin bir özetini görüntülemek isteyebiliriz.

- Doğru dosyayı mı düzenledik?
- Yanlışlıkla bir dosyayı sildik mi, silmedik mi?
- Olmaması gereken bir dosyayı ekledik mi, eklemedik mi? gibi.

`git status` komutu ile bu işlemi yerine getirebiliriz.

Bir sonraki aşamada değişen dosyalarımızdan hangilerinin **commit'e** dahil olup olmayacağını belirlememiz gerekiyor.

#### Staging Area (Depolama Bölgesi)

##### Eklemek

Bu adımda, **commit'e** dahil etmek istediğimiz dosyaları **stating area** denilen bir tampon bölgeye alırız.

Bu noktada ufak bir not;

- Dosyaların içeriği değişmiş değişmemiş
- Yeni dosya eklenmiş eklenmemiş

Bu dosyaların otomatik olarak **stating area'ya** eklenmenmesini sağlamaz. Bu işlem ile ilgili dosyaları seçerek biz bunu yapmalıyız.


Dosyalarımızı `git add . veya git add dosya-ismi.uzantisi` ile **stating area'ya** alabiliriz.


##### Çıkartmak

git add komutu ile **stating area'ya** aldığım bir değişikliği

```bash
git reset HEAD "dosya uzantisi"
```

komutu ile stating area'dan çıkartabilirim.

```bash
git rm -f “dosya uzantısı”
```

Dosyayı projeden tamamen silmiş olacağız.

---

Dosyalarımızı **stating area'ya** ekledikten sonra şimdi **commit** işlemine hazırız.

#### Git Commit

##### Düzenleme

Commit işlemini iki şekilde yapabiliyoruz; 

- `git commit -m "Committed message"`
- `git commit`

Birinci şekli ile kullanırsanız herhangi bir metin editörüne ihtiyaç duymaksızın 
komut satırı üzerinden commit işlemini tamamlayabilirsiniz.

İkinci şekilde ise metin editörü üzerinden yapacağız bu işi.

Commit ile dosyalarımızdaki değişiklikler; yeni bir versiyon olarak **Git'de** kayıt altına alınır.

Ekstra bilgiler:

- `git commit -amend -m “commit mesajı”
`

Son commit mesajını değiştirebiliriz.

##### Commitleri geri almak

- `git reset -hard`

Projede yapılan tüm değişiklikleri silip ve son commit edilen noktaya geri getirebiliriz.

- ` git reset [hash değerinin ilk 7 karakteri]`

Commitlediğimiz değişiklikleri geri almamızı sağlar. Bu işlemi yeni bir commit oluşturmadan yapar.

- ` git revert [hash değerinin ilk 7 karakteri]`

Commitlediğimiz bir değişikliği geri alırken projemizin tarihçesinden atmış olduğumuz commit’i silmez ve değiştirme işlemini yeni bir commit atarak gerçekleştirir.

Son işlem;

#### Git Push


{% include elements/figure.html image="https://encrypted-tbn0.gstatic.com/images?q=tbn%3AANd9GcTbI4MeBe_XLWbK2D2lLljn39dSBama4qOpDo5XLYl2pzhmsVHK" caption="Evde denemeyin." %}

- Değişiklikleri **stating area'ya aldık**
- Bu değişiklikleri commit ettik.
- `git push -u origin master` diyerek uzak repository'e yolluyoruz.


{% include elements/figure.html image="https://miro.medium.com/max/738/0*qmLRym9jZf4KJf--.jpg" caption="Git Workflow" %}


### Git Branch


Git **ağaç mantığı** ile çalışmaktadır.

Bir projeyi versiyonlamak istediğimizde git otomatik olarak master branch’ini oluşturur ve biz bu branch üzerinde çalışmaya başlamış oluruz.


{% include elements/figure.html image="https://miro.medium.com/max/3508/1*tnvRls6Dg7vFt0zGdtfu_w.png" caption="Git Branch Workflow" %}




> Neden branch'a gerek duyuyoruz?

- `git branch branchadı`
 
Bulunduğumuz branch’den yeni bir branch çıkabiliriz.

- `git branch`

Projedeki local branchleri görebiliriz.

- `git branch -v`

Projedeki local branchleri son commit bilgisi ile görebiliriz.

- `git branch -va`

Local’deki ve remote’daki branchleri liste halinde son commit bilgileri ile görebiliriz.

- `git checkout branchadı` komutuyla branch’ler arasında geçiş yapabiliriz.


Oluşturduğumuz branch’lerle işimiz bittiğinde veya başka bir nedenden dolayı bu branch’leri silmek isteyebiliriz. Local’deki bir branch’i silmek istersek

- `git branch -d branchadı` komutunu kullanabiliriz.

Silmek istediğimiz branch remote repository de ise

- `git push -d <remote_name> <branch_name>`


### Git Fetch

komutunu kullanarak **başka biri tarafından** değişiklik yapılıp yapılmadığına bakmamız gerekecektir. 

Projede aynı branch üzerinde çalıştığımız takım arkadaşlarımız var ise geliştirme yapmaya başlamadan önce bu komut yardımıyla `remote branch’deki tüm değişiklikleri local branch’imize almamız gerekir.`

Özetle;

Önce **git fetch** ile değişiklikleri çekiyoruz local repomuza.

**git diff** ile iki versiyon arasındaki farkları inceliyoruz.

Sorun yok ise, **git pull** ile workspace'e alıyoruz.

### Git Fetch vs Git Pull

Git fetch öncelikle değişiklikleri local repoya çeker fakat workspace' çekmez, **git diff** komutu ile kontrolü bize bırakır.

**Git pull** ise, doğrudan değişiklikleri local repoya alıp **commit'ler** böylece değişiklikler doğrudan workspace'e eklenir.

### Git Rebase ve Git Merge

init yahut clone komutu kullanın,

ilk branch daima **master'dır.**

**develop** branch'ı üzerinden geliştirme yapmaya başladığımda, bir noktada bu iki **branch'i** birleştirmek gerekiyor ki, yapmış olduğumuz tüm değişiklikleri **master branch'imde** görebilelim.

Bu işlemi gerçekleştirmek için dikkat etmemiz gereken tek bir nokta var.

Master branch’imden **development** branch’imi çıktıktan sonra bu branch’de herhangi bir değişiklik olup olmadığıdır.


{% include elements/figure.html image="https://miro.medium.com/max/1634/1*CePupxHsxULxsab4iV1AEQ.png" caption="Git Branch Workflow" %}

Master branch’imde herhangi bir değişiklik olmadıysa yani bu branch’in son commit’i ve development branch ile ortak commit’i aynı ise git;
- **git rebase** ile bu branch’i master ile birleştirebilirim.

**git checkout master** komutu ile master branch’ini head yapıyoruz. Daha sonrada **git rebase develop** komutu ile 
- master branch’ine develop branch’inin tüm tarihçesini aktarmış oluyoruz.

Develop branch’indeki tüm değişiklikler **artık master branch’imizdede** bulunuyor.

{% include elements/figure.html image="https://miro.medium.com/max/1736/1*YCUqtQ-Guqens9wzRaVfDw.png" caption="Git Branch Workflow" %}

---


Vermiş olduğum eğitime dair fotoğraflar:

{% include elements/figure.html image="https://raw.githubusercontent.com/enesusta/assets-host-for-github-pages/assets/28-02-2020-tarihli-git-egitimi/git-egitimi-1.jpeg" caption="Eğitimden #1" %}



{% include elements/figure.html image="https://raw.githubusercontent.com/enesusta/assets-host-for-github-pages/assets/28-02-2020-tarihli-git-egitimi/git-egitimi-2.jpeg" caption="Eğitimden #2" %}













































































---
title: Linux File System Permissions
tags: [Unix]
style: fill
color: light
description: Linux dosya sisteminin dosya izinlerine dair konfigürasyonları bu yazı ile anlayacaksınız.
---

Merhabalar. Başka bir yazı ile daha birlikteyiz yine.

**ls** komutunu `-l` parametresi ile çalıştırdığımızda dosya ve dizinler hakkındaki ayrıntılı bilgiyi edinebiliriz.

```bash
root@c3c800b5943a:/# ls -l
total 64
drwxr-xr-x   2 root root 4096 Feb 19 01:17 bin
drwxr-xr-x   2 root root 4096 Apr 24  2018 boot
drwxr-xr-x   5 root root  360 Mar  3 20:45 dev
drwxr-xr-x   1 root root 4096 Mar  2 14:08 etc
drwxr-xr-x   2 root root 4096 Apr 24  2018 home
drwxr-xr-x   1 root root 4096 May 23  2017 lib
drwxr-xr-x   2 root root 4096 Feb 19 01:15 lib64
drwxr-xr-x   2 root root 4096 Feb 19 01:14 media
drwxr-xr-x   2 root root 4096 Feb 19 01:14 mnt
drwxr-xr-x   2 root root 4096 Feb 19 01:14 opt
dr-xr-xr-x 140 root root    0 Mar  3 20:45 proc
drwx------   1 root root 4096 Mar  2 14:08 root
drwxr-xr-x   1 root root 4096 Feb 21 22:20 run
drwxr-xr-x   1 root root 4096 Feb 21 22:20 sbin
drwxr-xr-x   2 root root 4096 Feb 19 01:14 srv
dr-xr-xr-x  13 root root    0 Mar  3 20:45 sys
drwxrwxrwt   1 root root 4096 Mar  2 14:07 tmp
drwxr-xr-x   1 root root 4096 Feb 19 01:14 usr
drwxr-xr-x   1 root root 4096 Feb 19 01:17 var
```

İlk satırı ele alalım:

```bash
drwxr-xr-x   2 root root 4096 Feb 19 01:17 bin
```

Görselleştirir isek;

{% include elements/figure.html image="https://raw.githubusercontent.com/enesusta/assets-host-for-github-pages/assets/linux-file-system-permissions/permission1.svg?sanitize=true
" caption="ls -l" %}



- **1** numaralı bölge dosya ya da dizinle ilgili güvenlik bilgilerini.
- **2** numaralı bölge o dosya yada dizine bağlı olan bağlantı sayısını
- **3** numaralı bölge dosyanın / dizinin sahibi olan kullanıcını adını
- **4** numaralı bölge dosyanın / dizinin sahibi olan grup adını
- **5** numarali bölge dosya / dizinin **byte** cinsinden boyutunu
- **6** numaralı bölge dosya / dizinin düzenlendiği tarihi
- **7** numaralı bölge dosya / dizinin adını 

belirtir.


Bu örnek için birinci bölgemiz.



<p class="text-center text-secondary display-4 "> 
drwxr-xr-x
</p>

10 karakterlik bu ifadeyi **1 3 3 3** olarak bölmemiz gerekiyor.

**İlk** karakterimiz dosya tipini belirler, tabloyu inceleyin.

| Karakter | Anlamı |
| -- | -- |
| d  | dizin(directory) |
| -  | standart dosya |
|  l | bağlantı(link) |
| c | özel karakter dosyası(character) |
| b | özel blok dosyasını(binary) |

ifade eder.

Misal başka bir örnek için tekrar edelim;

```bash
root@c3c800b5943a:/# touch attempt.txt
root@c3c800b5943a:/# ls -l
total 64
-rw-r--r--   1 root root    0 Mar  3 21:36 attempt.txt (bu noktaya dikkat)
drwxr-xr-x   2 root root 4096 Feb 19 01:17 bin        
drwxr-xr-x   2 root root 4096 Apr 24  2018 boot       
drwxr-xr-x   5 root root  360 Mar  3 20:45 dev        
drwxr-xr-x   1 root root 4096 Mar  2 14:08 etc        
drwxr-xr-x   2 root root 4096 Apr 24  2018 home       
drwxr-xr-x   1 root root 4096 May 23  2017 lib        
drwxr-xr-x   2 root root 4096 Feb 19 01:15 lib64      
drwxr-xr-x   2 root root 4096 Feb 19 01:14 media      
drwxr-xr-x   2 root root 4096 Feb 19 01:14 mnt        
drwxr-xr-x   2 root root 4096 Feb 19 01:14 opt        
dr-xr-xr-x 135 root root    0 Mar  3 20:45 proc       
drwx------   1 root root 4096 Mar  2 14:08 root       
drwxr-xr-x   1 root root 4096 Feb 21 22:20 run        
drwxr-xr-x   1 root root 4096 Feb 21 22:20 sbin       
drwxr-xr-x   2 root root 4096 Feb 19 01:14 srv        
dr-xr-xr-x  13 root root    0 Mar  3 20:45 sys        
drwxrwxrwt   1 root root 4096 Mar  2 14:07 tmp        
drwxr-xr-x   1 root root 4096 Feb 19 01:14 usr        
drwxr-xr-x   1 root root 4096 Feb 19 01:17 var        
```

Yaratmış olduğumuz **attempt.txt** için 1 numaralı bölgenin 10 karakterini bu şekilde görüyoruz.

<p class="text-center text-secondary display-4 "> 
-rw-r--r--
</p>

İlk karakteri **-** dolayısı ile standart bir dosya olduğunu anlayabiliriz bu şekilde.


---

{% include elements/figure.html image="https://raw.githubusercontent.com/enesusta/assets-host-for-github-pages/assets/linux-file-system-permissions/permission2.png
" caption="" %}

Geriye kalan 9 karakteri üçer blok halinde parçalamıştık..

- Birinci blok sahibinin
- İkinci blok grubun
- Üçüncü blok ise geriye kalan kişilerin haklarını gösterir.

Bunlar;

- r: read(okuma),
- w: write(yazma),
- x: execute(çalıştırabilme)  

Yukarıdaki fotoğrafı incelersek birinci blokta şu şekilde bir hakka sahip;

<p class="text-center text-secondary display-4"> 
r w x
</p>


Bu da demek oluyor ki; **attempt.txt**'nin kullanıcısı bu dosyaya;
-  hem yazabilir
-  hem bu dosyayı okuyabilir
-  hem de bu dosyayı çalıştırabilir.


Dosya ve dizin haklarını **chown, chgrp** ve **chmod** komutları ile düzenleyebiliriz.

---

##### chown (change ownership)



Dosya ya da dizinin sahibini değiştirmek için kullanılır.

Komutun genel pattern'i,

`chown <kullanici adi|kullanici kodu> <dosya/dizin adi>`

Örnek vermek gerekirse;

**attempt.txt** dosyasının sahibini **enes** olarak değiştirir.

```bash
chown enes attempt.txt
```

`bin` dizininin ve altındaki `bütün dosya ve dizinlerin` sahibini **enes** olarak değiştirir.

```bash
chown -R enes /bin
```

Daha ayrıntılı bilgi için:

https://linux.die.net/man/2/chown


{% include elements/button.html link="https://github.com" text="GitHub" style="outline-dark" %}
































































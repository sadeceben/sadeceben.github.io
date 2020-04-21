---
layout: post
title:	"Ruby Nedir ?"
date:	2020-04-15 12:00:00
categories:
    - blog
tags:
    - ruby

---

![]({{ site.baseurl }}images/posts/2020/rubylogo.jpg )


### Ruby Nedir ?


Her şeyden önce nesneye yönelik bir script dilidir. bu dilin yapımcısı ( Yukuhiro Matsumoto ) amacı perlden daha güçlü, pythondan daha nesneye yönelik bir dil yapmaktı. Yapım nedeni ise ilginç, o dönemde ki mevcut programlama dillerin de istediğini bulamayınca yeni bir programlama dili tasarlamaya başlar. Bir çok programlama dilinden esinlenmiştir. Bunlar arasında Perl'de vardır. Bu arada pek teknik bir bilgi olmasada perl (inci) haziran ayının burç taşı. Ruby ise ondan sonra gelen temmuz ayının burç taşı olan Ruby (yakut)' dir.

Son olarak ruby'nin kendi resmi sitesine girdiğiniz de sizi bir söz karşılar

    > Bir programcının en iyi arkadaşı

Bence nedir sorusunun en iyi cevabı budur.

[**bakmak isteyene...**](https://www.ruby-lang.org/tr/)

### Avantajları nelerdir ?
Ruby ile istenileni kodlamak ( Gerçekten ) kolay. Benim en çok sevdiğim yapısı block tanımlarken ki esnekliği ve de parantez zorunluluğu olmaması.

Bu
```ruby
   def selamla(ad)
       puts "Selam, #{ad}"
   end

   selamla("sadeceben")
```
Ve bu
```ruby
   def selamla ad
       puts "Selam, #{ad}"
   end

   selamla "sadeceben"
```
Kod da çalışıcaktır. Ruby de kodlarken kurallara takılmazsınız. Ve kodlarken fark edeceksiniz ki bazı şeyleri tahmin etmeye başlıyorsunuz.
Mesela sistem zamanını yazdıralım
```ruby
def system_date
    puts Time.now.to_s
end

system_date
```
**Kodun Çıktısı :**

![Screenshot]({{ site.baseurl }}images/posts/2020/kodunçıktısı1.png)

Linux sistemler'de "system" parametresi ile linux komutları çalıştırmak mümkün olmakla beraber Windows sistemlerde ( Denemedim ) komut çalıştırabiliyor.
```ruby
#!/bin/ruby -w

   def scan ip
       system "nmap -sSV #{ip}"
   end

   ip = ARGV[0] || "localhost"
   scan ip
```
**Kodun çıktısı :**
![Screenshot]({{ site.baseurl }}images/posts/2020/kodunçıktısı2.png)


Aslında fark edemediğim ve hatırlamadığım o kadar çok avantajı var ki. İlerleyen yazılarımda anlatabilirim. Okuduğunuz için teşekkür ederim.



---
layout: post
title:	"Ruby İle Http Request Ve Base64 Örneği"
date:	2020-04-21 12:00:00
categories:
    - blog
tags:
    - ruby
---




Konuya başlamadan söylemeliyim. Ben linux tabanlı bir işletim sistemi  kullanıyorum ve yaptığım adımların bir kaç kısmı windowsta  çalışmayabilir. Şimdiden iyi okumalar...

# HTTP REQUEST ?

 Öncelikle http'den kısaca bahsedeyim. HTTP ( Hybertext Transfer Protocol ) , client ( istemci ) ve server ( sunucu ) arasında iletişim sağlayan  protokoldur. Bu iletişim şekline göre de bir çok method vardır. Ben  burada GET methoduyla istek gönderen bir kod yazacağım. Daha fazla  bekletmeden kodumuza geçelim.

Öncelikle burada yapmamız gereken bir kaç adım var.
**Birincisi :** 

```ruby
#!/bin/ruby -w
```

Burada yazacağımız dosyayı ne ile çalıştıralacağını gösterdik.  "-w" parametresi ne dersiniz ruby çalışırken ki bilgilendirme mesajını  yazmayı engeller ( Ruby version numarası vb...)
**İkincisi ise :**
 Kullanmış olduğum paketi ( httparty ) gem paket yöneticisi ile indirmek için terminal ekranına bunu yazalım.

```bash
sudo gem install httparty
```

Şimdi kodumuzu anlatmaya geçelim.

# HTTP REQUEST ( GET METHODS ) :

```ruby
#!/bin/ruby -w
require "httparty"

url = ARGV[0] || "null"

    if url != "null"
           res = HTTParty.get url
           if res.code.to_i == 200
               puts res.body.to_s
           else
               puts "kod : #{res.code.to_s}"
           end
    else
        puts "hata: argüman girmediniz"
    end
```

Kod çalışırken girilen **(url) argüman** linkine **get methodu** ile istek atıyoruz. İsteğimizin gidip gitmediğini ya da herhangi bir değişlikliğe uğrayıp uğramadığını anlamak içinse response **(res)** yani yanıtı yazdırmamız lazım.
 bunun içinse yanıt kodu "res.code.to_i" eğer (if) 200 dönerse (200 numaralı kod, http isteğinin başarılı bir şekilde bağlantı sağladığı anlamına gelir) sayfa içeriğini(res.body.to_s) ekrana yazdırıyoruz. Eğer ( else ) 200 dönmezse yanıt kodunu (res.code.to_s) ekrana yazdırıyoruz. Ve de hiçbir url ( Argüman ) girilmezse hata mesajı sizi karşılıyor. Yazdığım kod bu kadardı. Bu sadece get methodu için bir istekti. Daha bir sürü request türü var...

Meraklısı için [http request](https://www.w3schools.com/tags/ref_httpmethods.asp) türleri

(**Kodun Başarılı ( 200 ) Çıktısı :** 



![]({{ site.baseurl }}images\posts\2020\200.png)


 Bu kod ile diyeceklerim şimdilik bu kadardı. Sırada ki kodumuza geçelim...

# BASE64 ENCODE & DECODE
 Base64 nedir birazcık ondan bahsedeyim. **6 bit** ile ifade edilen **64 farklı** sayı, **ASCII** karakter kümesinde yazdıralabilir karakter ( **Printable Character**)  olarak ifade edilen ve aşağıda gösterilen 64 farklı karakterle  eşleştirilmiştir. Eldeki 6 bitlik verinin bu tablo ile eşleştirilmesi  ile **Base64 Encoding** yapılmış olur.

![]({{ site.baseurl }}images\posts\2020\base64.png)

Şimdi çok konuşmadan kodumuza geçelim.

# BASE64 ENCODE & DECODE :

```ruby
#!/bin/ruby -w 

require "base64"

prm = ARGV[0] || "null"
str = ARGV[1] || "null"


  if str.to_s != "null"

       if prm.to_s == "-e"
       puts Base64.encode64 str

       elsif prm.to_s == "-d"
       puts Base64.decode64 str

       else
       puts "parametre hatası ! " + "\nEncoding için -e yazınız.\nDecoding için -d yazınız."
       end

  else
       puts "hata : bir argüman girmediniz"
  end
```

Hadi gelin ne kodlamışım anlatmaya başlayayım. Öncelikle yukarıda bahsettiğim çalışma dosyasını tanımlayalım.

```ruby
#!/bin/ruby -w
```

daha sonra,
**Ruby**'nin kendine ait bir **base64 kütüphanesi** var onu tanımlamak için şunu yazalım. 

```ruby
require "base64"
```

Tamamdır bundan sonrası çok basit. Dışarıdan iki argüman alıyoruz ilk argümanımız (ARGV[0])  yani "prm" (parametre kelimesini "kendimce" kısaltım) bize decode mu yoksa encode mu yapacağımız söyleyecek. İkinci argümanımız ise  (ARGV[1]) yani "str" (String kelimesini kendimce kısalttım) bize encode ya da decode edilcek kelimeyi verecek. 

Eğer "||" karakterleri ) herhangi bir argüman eksik ya da girilmezse onlara "null" kelimesini (String) atayacak. Bundan sonrası daha da basit. Eğer (if) dedim "str"  "null" değerinden başka bir değer almışsa "-e" ise encode et, "-d" ise decode et. Herhangi bir hata durumunda ise "else" bloklarını çalıştır dedim.

**Bu da kodun çalışırken görseli :**

![]({{ site.baseurl }}images\posts\2020\çalışırjen.png)

**Bu da çalışmazken ki görseli :**

![]({{ site.baseurl }}images\posts\2020\çalışmazken.png)


 Beni buraya kadar okuduğunuz için **teşekkür ederim**. Şimdilik diyeceklerim bu kadar.

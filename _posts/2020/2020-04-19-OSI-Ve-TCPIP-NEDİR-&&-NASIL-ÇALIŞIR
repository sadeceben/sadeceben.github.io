---
layout: post
title:	"OSI Ve TCP/IP NEDİR && NASIL ÇALIŞIR ?"
date:	2020-04-19 12:00:00
categories:
    - blog
tags:
    - network
---



# OSI NEDİR && NASIL ÇALIŞIR ?

 İlk önce OSI ( **Open Systems Interconnections** ) modeli neden çıktı onu anlatalım. 1980 öncesinde iki cihazın  haberleşmesi için, o dönem bilgisayar donanımı üreten firmaların kendi  yaptıkları özel ağlar kullanıyordu.
 yani bu demek oluyor ki sadece o donanıma sahip cihazlarla iletişim sağlanabilir Mesela IBM'in SNA ( **System Network Architecture** ). İşte burada tam olarak OSI modeli fikri ortaya atılıyor. 
**Neden olmasın....** 
 OSI sayesinde  artık donanım üreten firmaların kendi özel ağlarını  kullanmamıza gerek kalmayacaktı. Artık iki bilgisayar iletişim  kurabilecekti. O zaman lafı uzatmadan gelin OSI nasıl çalışıyor  öğrenelim....

 OSI birbirleriyle **ardışık** bir şekilde **etkileşimli** yani alt görevli bir şekilde 7 **ayrı** katmandan oluşur.

**Sırasıyla katmanlar

 1 -****Physical Layer ( Fiziksel Katman )
 2 -****Data Link Layer ( Veri Bağlantısı Katmanı )
 3 -****Network Layer ( Ağ Katmanı )
 4 -****Transport Layer ( İletim Katmanı )
 5 -****Session Layer ( Oturum Katmanı )
 6 -****Prensentation Layer ( Sunum Katmanı )
 7 -****Application Layer ( Uygulama Katmanı )**



![]({{ site.baseurl }}images/posts/2020/osi.png )




**Şimdi bu sıraladığımız katmanları açıklayalım...

 ## Physical Layer ( Fiziksel Katman ) Nedir && Nasıl Çalışır ?

 Burada gelen verinin bitlere yani ikilik sayı sistemine ( sadece 0 ve 1  olan sayı sistemi ) çevrilmesinden ya da daha farklı bir deyişle verinin dijitalleşmesinden sorumludur . Tek amacı gelen verinin yapısına  bakmaksızın taşımaktır. Nasıl taşır diye sorarsanız ise cevap çok basit **internet kablolarıyla** .
 Tabi cevap basit ama arkada dönen durum biraz öyle değil . Veri bitleri  kablolarla iletilirken belli bir kurala göre iletilir. Bu iki kural iki  bilgisayar arasında kullanılmalıdır. Eğer kullanılmazsa iletişim  sağlanamaz veriler anlamsızlaşır. Peki nedir bu kural, Mesela bit  düzeyinde 1 sayısı +5 volt gücünde 2 milisaniyede gidecek .
 Eğer ki ikinci cihaz +7 volt 3 milisaniye şeklinde veriyi iletirse işte  burada iletişim sağlanamaz. ISO tam olarak ne iş yapar diye merak  ediyorsanız işte cevabı geliyor. ISO bu standartları sağlıyor. Bir  donanım firması ağ donanımı üretirken ISO'nun bu çıkardığı OSI modeline  göre üretim yapıyor. Bu katman hakkında diyeceklerim bu kadar şimdi  sırada ki katmana geçelim.

## Data Link Layer ( Veri Bağlantısı Katmanı ) Nedir && Nasıl Çalışır ?

 Bu katmanı anlatmadan önce katmanın daha iyi anlaşılması için kısaca ARP ( **Address Resulation Protocol** ) nedir ondan bahsedeyim . Kısaca ARP aynı ağda olduğumuz cihazların  MAC adresini bulmamıza yarayan bir protokoldür. Şimdi katmanı anlatmaya  geçelim.
 Veri bağlantı katmanında ARP protokolü ile fiziksel olarak  adreslenmesinden ve paketlerin fiziksel bağlantı sağlanan cihazlara  iletilimesinden sorumludur. Temel olarak görevi budur. Verilerin  kontrolü hata denetimi bu katmanda yapılır. CRC ( **Cyclic Redundancy Check** ) verilerin doğrulandığı bir sistemdir. Peki nasıl doğrular kısaca bahsedeyim. **Gelen veri** ile **alınan veri** aynı ise geçerlidir. Ama eğer yolda değiştirilmişse (**Örn: kötü amaçlı**) CRC bunu engeller. Buraya kadar anlattıklarımı özetlemek istersem aynı  ağda bulunan cihazların adreslenerek verinin güvenli bir şekilde  iletilmesini sağlar .

 Sırada ki katmana geçelim....

## Network Layer ( Ağ Katmanı ) Nedir && Nasıl Çalışır ?

 Bu katmanda mantıksal adresleme yapılırak uzakta ki cihazlara bağlantı  sağlanır. Peki nedir mantıksal adresleme. Mantıksal adresleme ilk  cümlemde de dediğim gibi uzakta ki cihazlarla iletşim kurmak için  kullanılan TCP/IP dediğimiz şeydir. IPV4 için 32 bit boyutunda IPV6 için 128 bit boyutundadır. Ve bu katmanda paket içinde bulunur.
 Bu katmanda IP ( Internet Protocol ) çalışır. Bu katmanda Routerlar  aracılığıyla paketler gideceği yere yönlendirilir . Üst katmandan gelen  mantıksal adreslemeler Fiziksel Adreslemeye dönüştürülür . Diyeceklerim  Bu kadardır. Sırada ki katmana geçebiliriz .

## Transport Layer ( İletim Katmanı ) Nedir && Nasıl Çalışır ?

 Taşıma katmanı adından da anlaşılacağı gibi verinin nasıl taşınacağına  karar verir. Üst katmandan gelen veri ağ paketi boyutunda ( Yani üst  katmandan gelen büyük veriyi küçük veriye çevirme ) getirilip bir alt  katman olan Network Layer iletilir . TCP ve UDP bu katmanda çalışır .
 Bu katmanda da hata kontrolü CRC çalışır. İletilemeyen veriler tekrardan iletilir. Ulaşılmış veriler de başarı mesajı verir .

## Session Layer ( Oturum Katmanı ) Nedir && Nasıl Çalışır ?

 Oturum katmanı yapılan işlemlerin başlatılmasından, sürdürülmesinden ve  de kapatılmasından sorumlu katmandır . Bu katmanın en can alıcı  özelliği, Bilgisayarımız aynı anda birden fazla cihazla iletişim halinde olduğunda doğru bilgisayarla iletişimde bulunmamızı sağlar. Bu bir üst  katmana gönderilecek verilere ayrı ayrı oturum açarak sağlarlar. Son  olarak bu katmanda socket'ler çalışır. Sırada ki katmanımıza geçelim.

## Prensentation Layer ( Sunum Katmanı )  Nedir && Nasıl Çalışır ?

 Sunuş katmanın en önemli özelliği verilerin karşı bilgisayarın  anlayacağı formata çevirmesidir. Bu sayede birbirinden farklı  programların iletişime geçmesini ( Birbirlerinin verilerini  kullanabilmesi ) sağlar. Verinin formatı belirlenir. Veriyi şifreleme,  sıkıştırma ve açma yine bu katmanda yapılır. Son katmanımıza geçelim.

## Application Layer ( Uygulama Katmanı ) Nedir && Nasıl Çalışır ?

 Uygulama katmanı bilgisayarda çalışan uygulamalar ile ağ arasında  iletişim görevi alır. OSI katmanları arasında bir tek bu diğer katmanlar ile iletşim halinde değildir. Kısaca görevi uygulamaların ağda sorunsuz çalışması için görev alır. SSH , telnet , http , https , SMTP , SNMP , DNS , FTP vb. servisler ve uygulamalar bu katmanda çalışır. Diyeceklerim bu kadar.

 Şimdi buraya kadar ne anlattım. Örnek içinde vermek gerekirse. Şimdi X  kullanıcı Y sunucusuna ssh ile bağlantı sağlıyacak. Burada ilk harekete  geçilecek nokta uygulama katmanında çalışan ssh programıdır. SSH  bağlantımız bu katmandan bilgisayara iletilir. Bağlantı sunum katmanında ssh bağlantısının isteği üzere gerekli format veya şekilde paketlenir.  Oturum katmanı bu iletişim için bir oturum başlatır. İletim katmanında  ise bağlantı isteğimiz segmentlere yani ( frame )'lere ayırarak  herbirinin başına ilgili verilerin hangi porttan bağlanılacağı gibi  bilgilerin eklediği PDU (protocol data unit) ekler. Parçalara ayrılan  bağlantının her bir segmenti ( frame ) ayrı ayrı alt katman olan ağ  katmanına iletilir. Ağ katmanı her bir parça için içerisinde kaynak ve  hedef IP adreslerinin ve diğer bilgilerin bulunduğu kendi PDU'sunu  ekler. Veri bağı katmanı kendisine gönderilen pakete kaynak ve hedef MAC adres bilgilerini ve diğer kontrol parametrelerini bulunduran kendi  PDU'sunu ekleyerek fiziksel katmana gönderir. Fiziksel katman kendisine  gönderilen tüm paketi 1ve 0 lardan oluşan bilgi katarı olarak bağlı  olduğu iletişim ortamına elektrik, radio sinyali veya ışık olarak  gönderir. Anahtarlama, yönlendirme işlemlerinden sonra hedefe ulaşan 1  ve 0 lardan oluşan bilgiler kaynak tarafında yapılan tüm işlemlerin  tersi yapılarak tekrardan uygulama katmanı ssh programı tarafından  kaydedilir.... Diyeceklerim bu kadar....



![]({{ site.baseurl }}images/posts/2020/osi.gif )




## OSI modelinin avantajları nelerdir ?

 öncelikle iki bilgisayarın ileteşim kurması artık daha kolay bir şekilde yapılabiliyor. Ve de verilerin iletiminde hata kontrol mekanizması ( **CRC** ) vardır. Verilerin iletimi belli bir standart haline getirelerek karmaşıklık önlenmiştir.

 Beni okuduğunuz için teşekkür ederim...

# TCP/IP Nedir && Nasıl Çalışır ?

 TCP/IP, TCP ( Transmission Control Protocol ) ve IP ( Internet Protocol ) ’nin birlikte çalışmasıdır. TCP sizin web tarayıcınız ile ağ  yazılımınız arasındaki haberleşmeye bakar. IP diğer bilgisayarlar ile  haberleşmeye bakar. TCP veriyi gönderilmeden önce IP paketlerine  ayrılmasından ve hedeflerine vardıklarında da bu paketlerin  birleştirilmesinden sorumludur. IP paketlerin alıcıya gönderilmesinden  sorumludur.

**Peki IP nedir...**

 IP, bilgisayarlar arası iletişim sağlamak için bağlantısız  (connectionless) bir haberleşme protokolüdür. İki bilgisayarın  birbirleriyle haberleşmesi esnasında herhangi bir haberleşme hattı  kullanmaz. Bu IP’nin ağ hatlarına olan ihtiyacını azaltır. Böylece her  hat aynı anda birden çok bilgisayarın birbirleri arasında haberleşmesi  için kullanılabilir. IP ile veriler birbirinden bağımsız küçük  “paketlere” ayrılır ve bilgisayarlar arasında internet aracılığıyla  gönderilir. IP, her paketin hedefine “yönlendirilmesinden” sorumludur.


 Yani kısaca anlatmak gerekirse TCP iki cihaz arasında iletişim yolu açar IP ise paketlerin doğru yere ulaşmasını sağlar....

**Şimdilik diyeceklerim bu kadar.**				 										 										 										 										 											 									 									

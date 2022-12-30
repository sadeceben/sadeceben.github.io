---
layout: post
title:	"AFK Defender"
date:	2022-12-20 12:00:00
categories:
- blog
tags:
- rust
- script
---
Öncelikle selam dostlar.
Uzun zamandır blog yazmadığımı ve bir çok hobimden
uzaklaştığımı farkettim.
Ve dahası bunu evde yatmam gereken bir dönemde anladım.

Çok fazla gevezelik etmeden, gelelim konumuza.
Bu yazımda sizlere günlük 
hayatımda beni rahatsız eden bir durumdan bahsedeceğim.
AFK (Away From Keyboard) kalma durumu. 
Öncelikle nedir 
[AFK](https://en.wikipedia.org/wiki/Glossary_of_video_game_terms#AFK) gelin ilk önce onu açıklayalım.
AFK(Away from keyboard), [kadim yazıtlarda](http://www.textfiles.com/fidonet-on-the-internet/878889/fido0619.txt) 
anlatılanlara göre 
1990 yılında bir haber sitesi ile  beraber
internet kültürüne dahil oldu.
AFK, "klavyeden uzakta" anlamına gelen bir kısaltmadır. 
Ne zaman AFK durumunda olacağımız ise uygulamadan uygulamaya fark göstermektedir.
Günümüz chat uygulamaları ve oyunlarında AFK, 
klavye ve mouse hareketlerinin 
belli bir süre kullanılmaması durumunda tetiklenmektedir.
Kısaca, geçici bir süre 
bilgisayardan uzakta kalma durumu olarak özetlenebilir.

Lakin bu durum beni oldukça rahatsız ediyor :D
5 - 10 dakikalığına pc başından kalkıyorum 
ve geri geldiğimde kendimi, 
bilgisayarım ya uyku modunda ya da 
oyun oynuyorsam afk engeline takılmış olarak buluyorum. 
Bende bu durum ile ilgili ufak bir script yazma ihtiyacı duydum.
Ve bu script, ekstra olarak rust ile olacaktı :D

Öncelikle ufak bi araştırma yapma ihtiyacı duydum.
Bunun sebebi, windows bir sistem yerine 
GNU/Linux bir sistem kullanıyordum.
GNU/Linux yaygın olarak xorg desteğini sunduğu 
için ona uygun bir kütüphane
var mı diye kontrol ettim.

Ve araştırmam sonucu sadece 1 tane bulabildim. 
[enigo](https://github.com/enigo-rs/enigo),
xorg 11'i hem klavye hem de mouse için destekliyor. 
Ama yeni nesil olan wayland desteği bulunmuyor. 
Zaten bir çok açıdan halen yetersiz 
[wayland](https://www.cbtnuggets.com/blog/technology/networking/why-use-wayland-versus-x11) :)
Kütüphanemizi bulmuştuk ama 
enigo'da ufacık bir problem vardı. 
Mouse konumunu alamıyordu.
Neden mouse konumu bizim için önemli bunu 
geliştirme esnasında anlatacağım.

Bu yüzden enigo'nun, 
forklanan repoları arasında gezinmeye başladım.
Ve [taaa daaa](https://github.com/Prunkton/enigo) buldum.
Bu repo kuracağım algoritma için birebir.
Hadi o zaman kolları sıvayalım 
ve şu lanet olası scripti yazalım :D


ilk iş olarak cargo ile bir dizin oluşturalım.
```bash
cargo new afk-defender --vcs none
```
`--vcs none` olma sebebi git, hg, pijul veya fossil 
gibi versiyon kontrol sistemlerinin repomuzda 
oluşturulmasını engellemek.
daha sonra `Cargo.toml` dosyasına gerekli 
kütüphaneleri ekleyelim.
```toml
[package]
name = "afk-defender"
version = "0.1.0"
edition = "2021"

# See more keys and their definitions at https://doc.rust-lang.org/cargo/reference/manifest.html

[dependencies]
enigo = { git = "https://github.com/Prunkton/enigo", branch = "master" }
clap = { version = "3.1.6", features = ["derive"] }
```
clap'ı burada anlatmayacağım, 
kısaca komut satırı argümanlarını pars eden bir kütüphane.
Kullanımı son derece basit.

Daha sonra `src/main.rs` dosyasına geçelim.

Öncelikle neleri import ettik gelin onlara bakalım.
- `clap`: komut satırı argümanlarını parse etmek için.
- `enigo`: mouse ve klavye işlemleri için.
- `std::thread::sleep`: threadlerin uyumasını sağlamak için.
yani kısaca, programızın beklemesi için.
- `std::time::Duration`: sleep fonksiyonuna 
verilecek parametreler için.
```rust
use clap::Parser;
use enigo::*;
use std::thread::sleep;
use std::time::Duration;
```
Burada yapacağımız şey, komut satırından 
`-t` veya `--timer` argümanını alıp 
hangi aralıklarda kontrol yapacağımızı programa söylemek.
```rust
/// nonesleep app
#[derive(Parser, Debug)]
#[clap(about, version, author)] // you can discard this if you want.
struct NoneSleep {
    /// sleep time in seconds
    #[clap(short = 't', long)]
    timer: u64,
}
```
`defend_ass` fonksiyonu, bizim için son derece önemli.
fonksiyonumuz, verilen x ve y koordinatlarına 
mousemuzu ışınlıyor. Bu nedenle uygulamalar bu ışınlanmayı
hareket olarak algıladığı için bizi
afk olmaktan kurtarıyor.
```rust
// move and click the mouse
fn defend_ass(x: i32, y: i32) {
let mut enigo = Enigo::new();
enigo.mouse_move_to(x, y);
}
```
gel gelelim main fonksiyonuna. 
Öncelikle clap için bir obje
oluşturuyoruz. Ardından timer argümanını alıyoruz.
sonra sonsuz döngüye giriyoruz ve 
ilk olarak mouse konumunu alıyoruz. 
Daha sonra girilen timer
değeri kadar bekliyoruz. 
Ardından tekrar mouse konumunu alıyoruz.
if bloğu mouse konumunun 
değişip değişmediğini, almış olduğumuz 
iki konuma ait x ve y kordinatlarını 
karşılaştırarak kontrol ediyor.

Eğer mouse konumu değişmemişse, mouse konumunu
bilgisayarın ilk pixeline ışınlıyor. Ve bizi afk olmaktan
kurtarıyor. Eğer değişmişse hiç bir işlem yapmadan 
devam ediyor.
```rust
fn main() {
    let value = NoneSleep::parse();
    let timer = value.timer;

    let mut enigo = Enigo::new();

    loop {
        let first_position = enigo.mouse_location();
        sleep(Duration::from_secs(timer));
        
        let second_position = enigo.mouse_location();
        if first_position == second_position {
            defend_ass(0, 0);
        }
    }
}
```

Kodun tüm hali aşağıda.
```rust
use clap::Parser;
use enigo::*;
use std::thread::sleep;
use std::time::Duration;

/// nonesleep app
#[derive(Parser, Debug)]
#[clap(about, version, author)] // you can discard this if you want.
struct NoneSleep {
    /// sleep time in seconds
    #[clap(short = 't', long)]
    timer: u64,
}

// move and click the mouse
fn defend_ass(x: i32, y: i32) {
    let mut enigo = Enigo::new();
    enigo.mouse_move_to(x, y);
}

fn main() {
    let value = NoneSleep::parse();
    let timer = value.timer;

    let mut enigo = Enigo::new();

    loop {
        let first_position = enigo.mouse_location();
        sleep(Duration::from_secs(timer));
        
        let second_position = enigo.mouse_location();
        if first_position == second_position {
            defend_ass(0, 0);
        }
    }
}
```
Ne kadar basit bir kod yazdık :D
Yok rustla iş uzar zart zurtculardansanız
fikriniz belki değişebilir.

Gelin bir de çalıştıralım.
```bash
cargo run -q -- -t 10
```
- `-q` argümanı, cargo'nun çıktılarını engellemek için.
- `-t` argümanı, timer'ı 10 saniye olarak ayarlamak için.

![Record]({{ site.baseurl }}images/posts/2022/record.gif)

Yazımın sonuna doğru, yeni yılın hepimiz için güzel ve 
sağlıklı bir şekilde geçmesini diliyorum. Unutmadan,
İşiniz gücünüz **rust** gitsin :D

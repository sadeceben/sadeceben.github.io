---
layout: post
title:  "Yazılım Tasarım Desenleri"
date:   2020-11-18 17:19:00
categories:
    - blog
tags:
    - software
---



## YAZILIM TASARIM MİMARİLERİ



### Dekoratör Tasarım Deseni : 

![]({{ site.baseurl }}images/posts/2020/desing_patterns/dekaretör_senaryo.png )

![]({{ site.baseurl }}images/posts/2020/desing_patterns/dekaretör_uml.png )



```C#
usingSystem;
usingSystem.Collections.Generic;
usingSystem.Linq;
usingSystem.Text;
usingSystem.Threading.Tasks;

namespace ConsoleApp2 {
	class DekoratörDeseni {
		interface IAraba {
			void bilgiDetayları ();
			void fiyatEkle(doubleeklenmişFiyat);
			void tanımEkle(stringeklenmişTanım);
		}
		public class Araba: IAraba {
			public string model { get; set; }
			public string marka { get; set; }
			public double fiyat { get; set; }
			public string tanım { get; set; }
			public Araba() {
				fiyat = 125.000;
			}
			public void bilgiDetayları () {
				Console.WriteLine(tanım);
			}
			public void fiyatEkle(double eklenmişFiyat) {
				fiyat += eklenmişFiyat;
			}
			public void tanımEkle(string eklenmişTanım) {
				tanım = "Model:" + model + " Marka: " + marka + " Güncel Fiyat: " + fiyat.ToString() + " " + eklenmişTanım;
			}
		}
		class ArabaDekoratör: IAraba {
			private IAraba araba;
			public ArabaDekoratör(IAraba a) {
				araba = a;
			}
			public void bilgiDetayları () {
				araba.bilgiDetayları ();
			}
			public void fiyatEkle(double eklenmişFiyat) {
				araba.fiyatEkle(eklenmişFiyat);
			}
			public void tanımEkle(string eklenmişTanım) {
				araba.tanımEkle(eklenmişTanım);
			}
		}
		class camTavanDekoratör: ArabaDekoratör {
			public camTavanDekoratör(IAraba araba) : base(araba) {}
			public void bilgiDetayları () {
				base.fiyatEkle(15);
				base.tanımEkle("camTavan bilgisi araca eklendi");
				base.bilgiDetayları ();
			}
		}
		class parkSensörüDekoratör: ArabaDekoratör {
			public parkSensörüDekoratör(IAraba araba) : base(araba) {}
			public void bilgiDetayları () {
				base.fiyatEkle(10);
				base.tanımEkle("parkSensörüaraca eklendi");
				base.bilgiDetayları ();
			}
		}
		static void Main(string[] args) { //Orjinal nesne
            IAraba araba = newAraba() { model = "Polo", marka = "Volkswagen", fiyat = 125.000, tanım = "Yeni araba eklendi"};
            //Nesneye cam tavan özelliğinin eklenmesi
            camTavanDekoratör camTavan = newcamTavanDekoratör(araba);camTavan.bilgiDetayları();
            //Park sensörü özelliğinin eklenmesi
            parkSensörüDekoratör parkSensörü= newparkSensörüDekoratör(araba);parkSensörü.bilgiDetayları();
			//Orjinal ikinci nesne
            IAraba araba2 = newAraba() { model = "S90", marka = "Volvo", fiyat = 240.000, tanım = "Yeni araba eklendi"};
            //Park sensörü özelliğinin eklenmesi
            parkSensörüDekoratör parkSensörü2 = newparkSensörüDekoratör(araba2);parkSensörü2.bilgiDetayları();}}}
			
```



###  Proxy Deseni :

Very soon!!!

### Adaptör Deseni :

Very soon!!!

### Cephe Deseni :

Very soon!!!




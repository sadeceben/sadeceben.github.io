---
layout: post
title:  "Yazılım Tasarım Desenleri"
date:   2020-11-18 17:19:26
categories:
    - blog
tags:
    - software
---



## YAZILIM TASARIM MİMARİLERİ



### Dekoratör Tasarım Deseni : 

![]({{ site.baseurl }}images/posts/2020/desing_patterns/dekaretör_senaryo.png )

![]({{ site.baseurl }}images/posts/2020/desing_patterns/dekaretör_uml.png )



```c#
usingSystem;
usingSystem.Collections.Generic;
usingSystem.Linq;
usingSystem.Text;
usingSystem.Threading.Tasks;

namespace ConsoleApp2 {
	class DekoratorDeseni {
		interface IAraba {
			void bilgiDetaylari ();
			void fiyatEkle(double eklenmisFiyat);
			void tanimEkle(string eklenmisTanim);
		}
		public class Araba: IAraba {
			public string model { get; set; }
			public string marka { get; set; }
			public double fiyat { get; set; }
			public string tanim { get; set; }
			public Araba() {
				fiyat = 125.000;
			}
			public void bilgiDetaylari () {
				Console.WriteLine(tanim);
			}
			public void fiyatEkle(double eklenmisFiyat) {
				fiyat += eklenmisFiyat;
			}
			public void tanimEkle(string eklenmisTanim) {
				tanim = "Model:" + model + " Marka: " + marka + " Guncel Fiyat: " + fiyat.ToString() + " " + eklenmisTanim;
			}
		}
		class ArabaDekorator: IAraba {
			private IAraba araba;
			public ArabaDekorator(IAraba a) {
				araba = a;
			}
			public void bilgiDetaylari () {
				araba.bilgiDetaylari ();
			}
			public void fiyatEkle(double eklenmisFiyat) {
				araba.fiyatEkle(eklenmisFiyat);
			}
			public void tanimEkle(string eklenmisTanim) {
				araba.tanimEkle(eklenmisTanim);
			}
		}
		class camTavanDekorator: ArabaDekorator {
			public camTavanDekorator(IAraba araba) : base(araba) {}
			public void bilgiDetaylari () {
				base.fiyatEkle(15);
				base.tanimEkle("camTavan bilgisi araca eklendi");
				base.bilgiDetaylari ();
			}
		}
		class parkSensoruDekorator: ArabaDekorator {
			public parkSensoruDekorator(IAraba araba) : base(araba) {}
			public void bilgiDetaylari () {
				base.fiyatEkle(10);
				base.tanimEkle("parkSensoruaraca eklendi");
				base.bilgiDetaylari ();
			}
		}
		static void Main(string[] args) { //Orjinal nesne
            IAraba araba = new Araba() { model = "Polo", marka = "Volkswagen", fiyat = 125.000, tanim = "Yeni araba eklendi"};
            //Nesneye cam tavan ozelliğinin eklenmesi
            camTavanDekorator camTavan = new camTavanDekorator(araba);
            camTavan.bilgiDetaylari();
            //Park sensoru ozelliğinin eklenmesi
            parkSensoruDekorator parkSensoru= new parkSensoruDekorator(araba);
            parkSensoru.bilgiDetaylari();
			//Orjinal ikinci nesne
            IAraba araba2 = new Araba() { model = "S90", marka = "Volvo", fiyat = 240.000, tanim = "Yeni araba eklendi"};
            //Park sensoru ozelliğinin eklenmesi
            parkSensoruDekorator parkSensoru2 = new parkSensoruDekorator(araba2);
            parkSensoru2.bilgiDetaylari();
 
       }
    }
 }

```



###  Proxy Deseni :

Very soon!!!

### Adaptör Deseni :

Very soon!!!

### Cephe Deseni :

Very soon!!!




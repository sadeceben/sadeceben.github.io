---
layout: post
title:  "Yazılım Tasarım Desenleri"
date:   2020-11-18 17:19:26
categories:
    - blog
tags:
    - software
---



## YAZILIM TASARIM MIMARILERI



### Dekorator Tasarim Deseni : 

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
            //Nesneye cam tavan ozelliginin eklenmesi
            camTavanDekorator camTavan = new camTavanDekorator(araba);
            camTavan.bilgiDetaylari();
            //Park sensoru ozelliginin eklenmesi
            parkSensoruDekorator parkSensoru= new parkSensoruDekorator(araba);
            parkSensoru.bilgiDetaylari();
			//Orjinal ikinci nesne
            IAraba araba2 = new Araba() { model = "S90", marka = "Volvo", fiyat = 240.000, tanim = "Yeni araba eklendi"};
            //Park sensoru ozelliginin eklenmesi
            parkSensoruDekorator parkSensoru2 = new parkSensoruDekorator(araba2);
            parkSensoru2.bilgiDetaylari();
 
       }
    }
 }

```



###  Proxy Deseni :

![]({{ site.baseurl }}images/posts/2020/desing_patterns/proxy_deseni.png )

````c#
using System;
namespace ConsoleApp2 {
	class Program {
		public interface INesne {
			string istek();
		}
		private class Nesne {
			public string istek() {
				return "Sol taraftaki kapiya git\n";
			}
		}
		public class Proxy: INesne {
			Nesne _nesne;
			public string istek() {
				if (_nesne == null) {
					Console.WriteLine("Robot inaktif durumdadir");
					_nesne = newNesne();
					return "Proxy sinifirobotun istegini bulamiyor. Lutfen robotu aktif ediniz. \n";
				}
				else Console.WriteLine("Robot aktif durumdadir");
				return "Proxy sinifirobotun istegini belirtiyor: " + _nesne.istek();
			}
		}
		public class korumaProxy: INesne {
			Nesne _nesne;
			string sifre = "hodor";
			public string dogrulama(string _s) {
				if (_s != sifre) return "Koruma Proxy: Sifre gecerli degil, erisim izni yok";
				else_nesne = new Nesne();
				return "Koruma proxy: Sifre gecerli, erisim saglandi";
			}
			public string istek() {
				if (_nesne == null) return "Koruma proxy: Ilk olarak dogrulama islemi gerceklestirinz";
				else return "Proxy sinifirobotun istegini belirtiyor: " + _nesne.istek();
			}
		}
		static void Main(string[] args) {
			INesne _nesne = new Proxy();
			Console.WriteLine(_nesne.istek());
			Console.WriteLine(_nesne.istek());
			_nesne = new korumaProxy();
			Console.WriteLine((_nesne askorumaProxy).dogrulama("Deneme"));
			Console.WriteLine((_nesne askorumaProxy).dogrulama("hodor"));
			Console.WriteLine(_nesne.istek());
			Console.ReadKey();
		}
	}
}
````



### Adaptör Deseni :

![]({{ site.baseurl }}images/posts/2020/desing_patterns/adaptör_deseni1.png )

```c#
using System;
namespace ConsoleApp5 {
	class Program {
		class Adapte {
			public double ozelIstek(double a, double b) {
				return a / b;
			}
		}
		interface IHedef {
			string istek(int i);
		}
		class Adaptor: Adapte,
		IHedef {
			public string istek(int i) {
				return "Sayinin yuvarlanmishali " + (int) Math.Round(ozelIstek(i, 3));
			}
		}
		static void Main(string[] args) {
			Adapte _adapte = new Adapte();
			Console.WriteLine("Yeni arayuzden once: ");
			Console.WriteLine(_adapte.ozelIstek(5, 3));
			IHedef _hedef = new Adaptor();
			Console.WriteLine("Yeni arayuz ile: ");
			Console.WriteLine(_hedef.istek(5));
			Console.ReadKey();
		}
	}
}
```



![]({{ site.baseurl }}images/posts/2020/desing_patterns/adaptör_deseni2.png )

```c#
using System;
namespace ConsoleApp6 {
	class Program {
		interface ISiparis {
			void siparis (string s);
		}
		class Adapte {
			public void ozelSiparis () {
				Console.WriteLine("Gitar siparisi basarilibir sekilde olusturulmustur... ");
			}
		}
		class Adaptor: Adapte,
		ISiparis {
			public void siparis (string s) {
				Console.WriteLine(s + " siparisi basarilibir sekilde olusturulmustur... ");
			}
		}
		static void Main(string[] args) {
			Adapte _adapte = new Adapte();
			_adapte.ozelSiparis ();
			ISiparis_siparis = new Adaptor();
			_siparis.siparis ("Keman");
			ISiparis_siparis2 = new Adaptor();
			_siparis2.siparis ("Tulum");
			ISiparis_siparis3 = new Adaptor();
			_siparis3.siparis ("Saz");
			Console.ReadKey();
		}
	}
}
```



### Cephe Deseni :

![]({{ site.baseurl }}images/posts/2020/desing_patterns/cephe_deseni.png )

```c#
using System;
namespace ConsoleApp3 {
	class Program {
		public class Gadget {
			public string islem1() {
				return "Gadget: Hazir\n";
			}
			public string islem2() {
				return "Gadget: Kalkisa Hazirlaniyor...\n";
			}
		}
		public class Spencer {
			public string islem1() {
				return "Spencer: Hazir\n";
			}
			public string islem2() {
				return "Spencer: AtesEtmeye Hazirlaniyor...";
			}
		}
		public class Cephe {
			protected Gadget _g;
			protected Spencer _s;
			public Cephe(Gadget altG, Spencer altS) {
				this._g = altG;
				this._s = altS;
			}
			public string Islem() {
				string sonuc = "Cephe  Tasarim Altsistemleri Baslatti\n";
				sonuc += this._g.islem1();
				sonuc += this._s.islem1();
				sonuc += "Cephe TasarimiAltsistemlere Komut Gonderiyor...\n";
				sonuc += this._g.islem2();
				sonuc += this._s.islem2();
				return sonuc;
			}
		}
		static void Main(string[] args) {
			Gadget altG = new Gadget();
			Spencer altS = new Spencer();
			Cephe cep = new Cephe(altG, altS);
			Console.WriteLine(cep.Islem());
		}
	}
}
```
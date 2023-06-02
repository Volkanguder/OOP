# OOP

### NYP'nin 4 Temel ilkesi

&emsp; Nesne yönelimli programlama dilinin nesne yöenlimli programlamayı uyguladığını anlamak için bu 4 temel ilkeyi sağlıyor olması gereklidir. Bu temel ilkeler kodların değiştirilebilirlik, yedinden kullanım ve esneklik gibi kriterlerin sağlanmasına ön ayak olurlar. Bu ilkeler;

**1. Encapsulation (Kapsülleme)**
**2. Ingeritance (Kalıtım)**
**3. Polymorphism (Çok Biçimlilik)**
**4. Abstraction (Soyutlama)**


------------

------------



# 1. Encapsulation (Kapsülleme)
&emsp; Bir sınıfa ait niteliklerin ancak o sınıfa ait metotlar tarafından değiştirilebilmesi ilkelsidir. Bu sayede nesnelere oluşacak anlamsızlıkların önüne geçilebilir.
&emsp; Ayrıca değişkenlere sınıfların dışından erişim olmaması ve bir sınıf içindeki değişkenlerin nasıl ve ne kadar olacağının da başka kodlardan saklanmış olması anlamına gelir. Böylelijler değişkenlerimizi sarmalayarak istenmeyen durumlardan korunacak bir filtre haline dönüştürebiliriz.

## Erişim Belirleyiciler (Access Modifier)
&emsp; Bir sınıfa nitelik ve davranışlara ulaşabilmek için **Erişim Belirleyiciler (Access Modifier)** kullanılır. Erişim belirleyiciler, değişken, metot ve sınıfların önüne yazılır ve yazıldıkları konuların erişebilecekleri alanları belirler.

- **Private (-) :**
> &emsp; Yazıldığı öğenin sadece ait olduğu sınıftan doğrudan erişilebilir olduğunu ve o sınıfın dışındaki kod parçacıklarından doğrudan erişim izni olmadığını tanımlar.

- **Public (+) :**
> &emsp;  Yazıldı öğenin sadece ait olduğu sınıf için değil, diğer sınıflar tarafından doğrudan erişilebilir olmasını sağlar. Sınıflara ait nesnelerin ve diğer nesneler tarafından kullanılmasını istenilen metotlar için kullanılır.

- **Protected :**
> &emsp;  `public` ve `private` arasında kalan bir erişim düzenleyicidir. Protected ile tanımlanan öğeler, kendisi ile aynı pakette (package) bulunan sınıflar tarafından doğrudan erişilebilir


------------


## Encapsulation (Kapsülleme) Örnek
&emsp;  Kitap adında bir sınıfımız olsun ve bu sınıfımıza ait 3 adet değişkenimiz olsun bunlar ; kitapAdi, sayfaSayisi ve yazar. Bu değişkenlerin erişim belirleyicileri public olsun ve her sınıftan erişilsin. Kitap sınıfından oluşturacağımız bir nesne bu niteliklerin hepsini taşısın. Bu yüzden oluşturacağımız Constructor (kurucu) metodunu bu şekilde oluşturalım.

|<center>Kitap</center>|
| :------------ |
|+ kitapAdi : string<br>+ sayfaSayisi : int<br>+ yazar : string|
|<br><br><br>|

```java
public class Kitap {
    public int sayfaSayisi;
    public String kitapAdi, yazar;
    Kitap(String kitapAdi, int sayfaSayisi, String yazar) {
        this.kitapAdi = kitapAdi;
        this.sayfaSayisi = sayfaSayisi;
        this.yazar = yazar;
    }
}
```
&emsp;  Görüldüğü üzere normal bir sınıfımız ve kurucu metodumuz var. Kitap sınıfından bir nesne oluşturalım.
```java
Kitap book = new Kitap("Harry Potter", 500, "JK Rowling");
```
&emsp;  Kitap sınıfından **book** adlı bir nesne oluşturduk ve bu nesnemizin niteliklerini belirttik. Peki biz bu kurucu metotta sayfa sayısını negatif bir değer girseydik ne olurdu ? Hiç bir kitabın sayfa sayısı negatif bir değer olamayacağı için, nesnemizde bir **anlamsızlık** olacaktı. Biz bu sorunu **constructor (kurucu)** metotumuza yazacağımız bir **if** kontrolü ile çözebiliriz.
```java
public class Kitap {
    public int sayfaSayisi;
    public String kitapAdi, yazar;
    Kitap(String kitapAdi, int sayfaSayisi, String yazar) {
        this.kitapAdi = kitapAdi;
        this.yazar = yazar;
        if (sayfaSayisi < 1) {
            this.sayfaSayisi = 10;
        } else {
            this.sayfaSayisi = sayfaSayisi;
        }
    }
}
```
&emsp;  **Constructor** metodu görüldüğü gibi modifiye ettik ve nesne oluşturulurken anlamız verilerin olmasını engelledik. Ama sorunlarımız hala bitmedi , biz nesneye ait niteliklere hala dışarıdan erişebiliyoruz ve `book.sayfaSayisi = -10` dersek , nesneye ait sayfa sayısını yine anlamsızlaştırmış oluruz. Bu sorunu çözmek için sınıfa ait değişkenlere dışarıdan erişimi kapatmamız gerekir ve oluşturduğumuz değişkenlerin** erişim belirleyicilerini (Access Modifiers)** değiştirmemiz gerekli. Tüm **public'leri private** olarak değiştiriyoruz.

&emsp;  Sınıfımızın son hali

|<center>Kitap</center>|
| :------------ |
| - kitapAdi : string<br>- sayfaSayisi : int<br>- yazar : string |
| + Kitap(kitapAdi,sayfaSayisi,yazar)<br><br><br> |

```java
public class Kitap {
    private int sayfaSayisi;
    private String kitapAdi, yazar;
    Kitap(String kitapAdi, int sayfaSayisi, String yazar) {
        this.kitapAdi = kitapAdi;
        this.yazar = yazar;
        if (sayfaSayisi < 1) {
            this.sayfaSayisi = 10;
        } else {
            this.sayfaSayisi = sayfaSayisi;
        }
    }
}
```


&emsp;  Sınıfa ait değişkenlerimin izinlerini **private** yaparak bu sorunu çözdük ama, biz book nesnesine ait değişkenlere erişimi tamamen kısıtladık. Yani biz oluşturduğumuz nesneye ait sayfa sayısını ekrana bastıramayız çünkü değişken **private** olarak tanımlandı. Ya da sayfa sayısı yanlış girilmiş bir nesneyi daha sonrasında düzenleyemeyiz. Bu sorunu çözmek için sınıfa ait değişkenlerimizi **sarmalayarak**, sınıf içerisinde ki **metotlar** yardımı ile değişkenlerimizi **koruma** altına alıyoruz ve kullanıma sunuyoruz. Bu metotlara sonrasında ismini çok duyacağımız **Getter** ve **Setter** metotları diyoruz.

## Getter ve Setter Metotları

|<center>Kitap</center>|
| :------------ |
| - kitapAdi : string<br>- yazar : string<br>- sayfaSayisi : int |
| + Kitap(kitapAdi,yazar,sayfaSayisi)<br> + getKitapAdi(): string<br> + setKitapAdi(String KitapAdi) : void<br> + getYazar() : string<br>+ setYazar() : void<br> + getSayfaSayisi() : int<br>+ setSayfaSayisi() : void  |

### Getter
&emsp;  Sınıfımıza ait **private** değişkenler mevcut. Bu değişkenlere dışarıdan erişebilmek için **her bir değişkenimiz** için **Getter** metodu yazmalıyız. Nesneye ait bu metot çağrıldığında geriye bir değer döndürmeli ve bu değer bizim istediğimiz **private** değişken olmalı. `sayfaSayisi` değişkeni için **getter** metodu tanımlayalım,
```java
public class Kitap {
    private int sayfaSayisi;
    private String kitapAdi, yazar;


    Kitap(String kitapAdi, int sayfaSayisi, String yazar) {
        this.kitapAdi = kitapAdi;
        this.yazar = yazar;
        if (sayfaSayisi < 1) {
            this.sayfaSayisi = 10;
        } else {
            this.sayfaSayisi = sayfaSayisi;
        }
    }

    public int getSayfaSayisi() {
        return this.sayfaSayisi;
    }
}
```
&emsp;  Görüldüğü gibi basit bir metot yardımı ile sınıfa ait **private** değişkenimize ulaşabildik. Burada dikkat edilmesi gereken noktalar **getter** metotları **geri dönüşü** olan metot tipindedir ve isimlendirilmesi ise **get** ile başlayıp sonra değişken ismi yazılmalıdır. İsimlendirmeyi bu şekilde yapmasak da çalışacaktır lakin kodun okunabilirliği adına bu kurala uyulması **gerekir**.

### Setter
&emsp;  Biz **getter** metodu ile **private** olan değişkenimize ulaştık.Peki bu değişkenin değerini değiştirmek istediğimizde ne yapmalıyız ? Bir sınıfa ait **private** bir değişkenin değerini değiştirmek için, setter metodu yazılmalıdır. `sayfaSayisi` değişkeni için **setter** metodu yazalım.
```java
public class Kitap {
    private int sayfaSayisi;
    private String kitapAdi, yazar;


    Kitap(String kitapAdi, int sayfaSayisi, String yazar) {
        this.kitapAdi = kitapAdi;
        this.yazar = yazar;
        if (sayfaSayisi < 1) {
            this.sayfaSayisi = 10;
        } else {
            this.sayfaSayisi = sayfaSayisi;
        }
    }

    public int getSayfaSayisi() {
        return this.sayfaSayisi;
    }

    public void setSayfaSayisi(int sayfaSayisi) {
        this.sayfaSayisi = sayfaSayisi;
    }
}
```
&emsp;  Görüldüğü üzere **setter** metodu sadece değiştirme işlemi yapacağı için **void** olarak tanımlandı ve bir adet parametre aldı. Bu parametre bizim yeni değerimi taşıyor olup, sınıfa ait değişkene aktarılmıştır. Ama burada hala bir sorun söz konusudur, bizler **setter** metodunu kullanarak sayfa sayısını negatif girebiliriz. Bu sorunu aşmak için **constructor (kurucu)** metotta yaptığımız gibi bir **if** koşulu ile bu sorunu çözebiliriz.
```java
public class Kitap {
    private int sayfaSayisi;
    private String kitapAdi, yazar;


    Kitap(String kitapAdi, int sayfaSayisi, String yazar) {
        this.kitapAdi = kitapAdi;
        this.yazar = yazar;
        if (sayfaSayisi < 1) {
            this.sayfaSayisi = 10;
        } else {
            this.sayfaSayisi = sayfaSayisi;
        }
    }


    public int getSayfaSayisi() {
        return this.sayfaSayisi;
    }


    public void setSayfaSayisi(int sayfaSayisi) {
        if (sayfaSayisi < 1) {
            this.sayfaSayisi = 10;
        } else {
            this.sayfaSayisi = sayfaSayisi;
        }
    }
}
```
&emsp;  **Setter** metodunu modifiye ederek nesnemiz için anlamsız olan durumu ortadan kaldırmış olduk. **Setter** metodunun genel özellikleri ise , geriye bir değer döndürmeyen metot olması ve isimlendirme yaparken başlangıç olarak set yazıp sonrasında değişken ismini yazmaktır.

&emsp;  Bu örnekteki `sayfaSayisi` değişkenini koruma ve anlamsızlaşmasını önlemek için **Nesne Yönelimli Programlamanın** ilkesi olan **Encapsulation (Sarmalama/Kapsülleme)** ilkesinden yararlandık. Bir sınıfa ait değişkenlerimizi **Getter** ve **Setter** metotları yardımı ile sarmaladık ve istenilen şartlara göre oluşmasını sağladık.

------------

------------

# 2. Inheritance (Kalıtım)
&emsp;  Kalıtım, programlama ortamında da gerçek hayattaki tanımına benzer bir işi gerçekleştirir. Bir sınıfın başka bir sınıftan kalıtım yapması demek, kalıtımı yapan sınıfın diğer sınıftaki nitelik ve davranışlarını kendisine alması demektir. Kalıtımı yapan sınıfa **alt sınıf**, kendisinden kalıtım yapılan sınıfa **ata sınıf** dersek, ata sınıfta tanımlı olan her şeyin alt sınıf için de tanımlı olduğunu söyleyebiliriz.

Eğer bir A sınıfın B sınıfından kalıtım yapması isteniyorsa, aşağıda ki şekilde tanımlanır.
```java
public class A extends B {
     // 
}
```
## Kalıtım Türleri
### Tek Yönlü Kalıtım (Single Inheritance)
&emsp;  Bir sınıfın başka bir sınıfı genişlettiği alt ve ata sınıf ilişkisini ifade eder.

![1](https://github.com/Volkanguder/OOP/assets/67462858/463b57e8-c3e9-4159-8f2d-09b25eb0d153)

&emsp;  Bu örnekte B sınıfı A sınıfını miras alır.

### Çoklu Kalıtım (Multiple Inheritance)
&emsp;  Bir sınıfın birden fazla sınıfı miras almasını ifade eder; bu, bir alt sınıfın iki ata sınıfa sahip olduğu anlamına gelir.

> Not : Java çoklu kalıtımı desteklemez. (Interface kullanılır)

![2](https://github.com/Volkanguder/OOP/assets/67462858/0efd8e50-afca-49fe-90cc-d52cfe5a48f3)

### Çok Seviyeli Kalıtım (Multilevel Inheritance)
&emsp;  Bir sınıfa ait alt sınıfın başka sınıfları genişletmesine denir.

![3](https://github.com/Volkanguder/OOP/assets/67462858/0a8ac68f-1dbd-4440-be77-b24552c5acdb)

Bu örnekte , C sınıfı B sınıfını miras alır, B sınıfı ise A sınıfını miras alır. C sınıfı dolaylı yoldan A sınıfını da miras almış olur.

### Hiyerarşik Kalıtım (Hierarchical Inheritance)
&emsp;  Birden fazla sınıfın aynı sınıfı genişlettiği bir alt ve üst sınıf ilişkisini ifade eder.

Bu örnekte : B, C ve D sınıfları aynı A sınıfını genişletir.

![4](https://github.com/Volkanguder/OOP/assets/67462858/9d4477da-fc69-491d-a6fd-c7f0e01c383f)

### Hibrit Kalıtım (Hybrid Inheritance)
&emsp;  Programda birden fazla kalıtım türünün kombinasyonuna denir. Örneğin, A ve B sınıfı, C sınıfını genişletir ve başka bir D sınıfı, A sınıfını genişletir, bu bir hibrit kalıtım örneğidir, çünkü bu, tek yönlü ve hiyerarşik kalıtımın bir birleşimidir.

### Kalıtım'da Constructor Zinciri ve Super Anahtar Sözcüğü
&emsp;  Bir sınıfa ait nesne oluşturulurken, o sınıfın bir kurucusunun işletildiğini, kurucunun çalışması tamamlandıktan sonra bellekte artık bir nesnenin oluştuğunu biliyoruz. Kurucuları da nesneleri ilk oluşturuldukları anda anlamlı durumlara taşıyabilmek için kullanıyoruz. Bu durumda, eğer nesnesi oluşturulacak sınıf başka bir sınıfın alt sınıfıysa, önce ataya ait iç nesnesinin oluşturulması ve bu nesnenin niteliklerinin ilk değerlerinin verilmesi gerektiğini söyleyebiliriz.
&emsp;  İç içe nesnelerin oluşabilmesi için nesnelerin içten dışa doğru oluşması gerekir. İç-nesnenin oluşabilmesi için, nesnesi oluşturulacak sınıfa ait kurucu işletilmeye başladığı zaman ilk iş olarak ata sınıfa ait kurucu çağrılır. Eğer ata sınıf da başka bir sınıfın alt sınıfıysa, bu kez o sınıfın kurucusu çağrılır. Kurucu zinciri alt sınıftan ata sınıfa doğru bu şekilde ilerler. En üstte, kalıtım ağacının tepesindeki sınıfın kurucusunun çalışması sonlandıktan sonra sırası ile alt sınıfların kurucularının çalışması sonlanacaktır. Böylece iç içe nesneler sıra ile oluşturularak en son en dıştaki nesne oluşturulmuş olur ve kurucu zinciri tamamlanır.

### Super Kullanımı
&emsp;  Eğer ata sınıfta varsayılan kurucu yoksa ve programcı alt sınıftaki kurucunun içinde ata sınıfın hangi kurucusunun çağrılacağını belirtmezse derleme hatası alınacaktır. Çünkü derleyici aksi belirtilmedikçe ata sınıfın varsayılan kurucusunu çağıran super() kodunu üretecektir. Ata sınıfın hangi kurucusunun çağrılacağı, super anahtar sözcüğü ile birlikte verilen parametrelere göre belirlenir. Nasıl ki new işleci ile birlikte kullandığımız parametreler hangi kurucunun çağrılacağını belirliyorsa, super anahtar sözcüğü ile birlikte kullanılan parametreler de aynı şekilde ata sınıfın hangi kurucusunun işletileceğini belirler.


------------


------------




# 3. Polymorphism(Çok Biçimlilik)
&emsp;  Polymorphism(çok biçimlilik) NYP'de programlama dilinin farklı tip verileri ve sınıfları farklı şekilde işleme yeteneğini belirten özelliğidir. Daha belirgin olmak gerekirse, metotları ve türetilmiş sınıfları yeniden tanımlama yeteneğidir.

&emsp;  Polimorfizm, alt sınıfların ata sınıflardaki metotları geçersiz kılması(method overriding) sayesinde çok biçimli olarak davranmasına denir. Bu sayede alt sınıf ata sınıfından gelen davranışı kendine göre şekillendirebilir.

&emsp;  Metotlarda "Geçersiz Kılma" ise bir alt sınıfın içine doğrudan ya da dolaylı ata sınıflarından gelen bir(ya da daha fazla) yöntemin aynısının(aynı yöntem adı ve aynı parametre listesi) kodlanmasına verilen addır.

&emsp;  Polimorfizm sayesinde uygulamaların genişletilebilirliğini sağlarız ve bir ata sınıfın sunduğu yöntemleri geçersiz kılan alt sınıflar yardımı ile ata sınıfa göre kodlanmış tek bir kod kesimine farklı davranışlar yüklemek olanaklı olmaktadır. Öyleyse, elimizde esnek bir altyapı var demektir. Bu esneklik altyapıya yeni türlerin eklenmesi, kalıtım ve geçersiz kılma ilişkileri çerçevesinde oldukça kolaydır.

**Polimorfizm Örneği**

![polimorfizm](https://github.com/Volkanguder/OOP/assets/67462858/f3499f50-47c2-493c-8e7f-cfe2614e5cbc)


------------


------------

# Abstraction (Soyutlama)
&emsp;  Nesne yönelimli programlamada Soyutlama (Abstraction) ilkesi, eğer bir sınıf için nesne üretmek mantıksız geliyorsa o sınıf soyutlanabilir. Alt sınıfların ortak özelliklerini ve işlevlerini taşıyan ancak henüz bir nesnesi olmayan bir üst sınıf oluşturmak istenirse bir soyut (abstract) üst sınıf oluşturulur.

&emsp;  Soyutlama, bir sınıfa veya metoda temel görevlerin tanımlanması, detayların ise tanımlanmaması demektir. Temel olarak bir soruna ait çözüme giderken kullanılacak yöntemlerin, ilk etapta daha genel basit ve soyut bir tanımını yapmaktır.

"abstract" Anahtar Kelimesi ve Soyut Sınıf Kavramı (Abstract Class)
Soyutlama kavramı sınıfın içindeki iç işleyişi dışarıdan izole etmek, yani gizlemektir. Örneğin: bilgisayarı kullanırken çoğu kullanıcı bilgisayarın iç işleyişinden haberi olmaz. Hafızanın işlemciyle haberleşmesi, işlemler arası senkronizasyon, klavyeden girilen değerlerin ekrana yansıması gibi birçok işlemin detayı kullanıcılardan gizlenmiş durumdadır. Kullanıcılar sadece bu fonksiyonları veya işlevleri bir arayüz vasıtasıyla çağırıp kullanmaktadır. İç detaylarına müdahale etmemektedir.

&emsp;  Aynı şekilde Java'da sınıflarımızı tasarlarken bazı fonksiyonların ve işlevlerin sadece sınıf içinde kalması, dış dünyada bu sınıftan nesneleri kullanan kişilerin bu iç fonksiyonları bilemelerine gerek yoktur. Örneğin: KDV tutarını hesaplayan fonksiyonun sınıf içinde kullandığı birçok başka fonksiyon olabilir. Bu fonksiyonların sınıf dışına açılmasının bir anlamı yoktur. Sadece miktarı verip o miktara göre KDV tutarını hesaplayacak bir dış fonksiyon yeterlidir. Yazılım dünyasında bu nedenle soyutlama kavramı yazılım tasarımında önemli bir kavramdır. Soyutlama yapabilmek için "abstract" anahtar kelimesi, "interface" gibi yapılar bizlere yardımcı olmaktadır.

**Soyutlama için Java'da iki yöntem mevcuttur:**
- "interface" tanımlamak
- "abstract" sınıf tanımlamak

##Soyut Sınıf (Abstract Class)
&emsp;  "abstract" anahtar kelimesi ile tanımlanan sınıflardır. Sınıfın içinde soyut ("abstract") metotlar veya normal fonksiyonlar tanımlanabilir. Soyut sınıflardan "new" anahtar kelimesi ile bir nesne oluşturulamaz.

### Soyut Sınıf Özellikleri:
- "abstract" anahtar kelimesi ile tanımlanmış olması gerekiyor.
- Soyut veya soyut olmayan fonksiyonlar tanımlanabilir.
- Soyut sınıflardan "new" anahtar kelimesi ile nesne oluşturulamaz.
- Kurucu metodu ve static fonksiyonlar tanımlanabilir.
- "final" kelimesi ile tanımlanmış fonksiyonları içerebilir. Bu final fonksiyonlar alt sınıflarda ezilemezler (override).

```java
// abstract sınıf örneği
public abstract class Doping {

	protected double price;
	protected double[] taxes;

	public double[] getTaxes() {
		return taxes;
	}

	public void setTaxes(double[] taxes) {
		this.taxes = taxes;
	}

	public double getPrice() {
		return price;
	}

	public void setPrice(double price) {
		this.price = price;
	}

	// soyut metot örneği
	public abstract double calculate();
}
```

&emsp;  Yukarıda soyut bir sınıf tanımladık. "abstract" kelimesi ile sınıf tanımladık, ayrıca sınıfın içinde "calculate" isimli "abstract" metot tanımladık. Aynı zamanda soyut olmayan metotlar da tanımladık. Senaryomuzda bir e-ticaret sisteminde "Doping" tipinde ek ürünler olduğunu düşünelim. İlan tarihini güncelleyen bir doping çeşidimiz olsun, bir de üst sırada çıkmanızı sağlayan bir doping olsun. Bu iki alt sınıfta "Doping" isimli sınıftan kalıtım alarak belli özellikleri kendilerine alsınlar. Fakat, her dopingin ücret hesaplama yöntemi birbirinden farklı olabilir. Ayrıca, her dopingin mutlaka fiyat hesaplama fonksiyonu olmalıdır.

&emsp;  Yukarıdaki durumda "abstract" sınıf tanımlayıp diğer doping çeşitleri bu ATA sınıftan kalıtım alacaklardır. "calculate" isimli "abstract" metodu, "metod ezme" (overriding) yöntemiyle ezip metodun içini kendilerine göre dolduracaklardır. Alt sınıflardaki diğer özellikler soyutlama tekniğiyle dış dünyadan gizlenecektir. Dış dünyadan dopingi kullanmak isteyen baka bir sınıf veya kod parçası doping nesnesi üzerindeki "calculate" fonksiyonunu çağırıp fiyatı hesaplayacaktır. Diğer iç hesaplama ve çalışma detaylarını bilmeyecektir.

```java
public class TopOfListDoping extends Doping {

	public TopOfListDoping(double price) {
		super.setPrice(price);
	}

	// "Doping" soyut sınıfından kalıtımla gelen, "calculate" isimli soyut metodu metot ezmesi yöntemiyle alt sınıf kendi ihtiyacına göre dolduruyor.
	// "TopOfList" isimli doping tipinde vergiler olmadığı için komisyon oranı eklenip ücret hesaplanıyor. Fakat, başka doping çeşitlerinde hesaplama farklı olabilir.
	@Override
	public double calculate() {

		return super.getPrice() + super.getPrice() * 0.35;
	}
}

public class UptodateDoping extends Doping {

	public UptodateDoping(double price, double[] taxes) {
		super.setPrice(price);
		super.setTaxes(taxes);
	}

	// "Doping" soyut sınıfından kalıtımla gelen, "calculate" isimli soyut metodu metot ezmesi yöntemiyle alt sınıf kendi ihtiyacına göre dolduruyor.
	// "UptodateDoping" isimli doping tipinde vergiler fiyata dahil olduğu için komisyon oranı eklenip ve vergiler hesaplanıp ücret belirleniyor.
	// Görüldüğü gibi her doping çeşidinin fiyat hesaplama yöntemleri birbirinden farklıdır. Soyutlama ile sınıflara ait iç çalışma detayları gizlenmmiş oluyor.
	// Doping tiplerinde sadece "calculate" isimli fonksiyonu dış dünyaya açtık. Diğer tüm fonksiyonlar ve özellikler sınıf içinde kaldı.
	@Override
	public double calculate() {
		
		return calculateTaxes() + commisionRate();
	}

	private double calculateTaxes() {
		
		double totalTaxValue = 0;
		for(int i=0; i < super.getTaxes().length; i++) {
			totalTaxValue += super.getTaxes()[i];
		}
		return totalTaxValue;
	}

	private double commisionRate() {
		return super.getPrice() * 0.2;
	}
}
```

&emsp;  "Doping" soyut sınıfından kalıtımla gelen, "calculate" isimli soyut metodu metot ezmesi yöntemiyle alt sınıf kendi ihtiyacına göre dolduruyor. "UptodateDoping" isimli doping tipinde vergiler fiyata dahil olduğu için komisyon oranı eklenip ve vergiler hesaplanıp ücret belirleniyor. Görüldüğü gibi her doping çeşidinin fiyat hesaplama yöntemleri birbirinden farklıdır. Soyutlama ile sınıflara ait iç çalışma detayları gizlenmiş oluyor. Doping tiplerinde sadece "calculate" isimli fonksiyonu dış dünyaya açtık. Diğer tüm fonksiyonlar ve özellikler sınıf içinde kaldı.


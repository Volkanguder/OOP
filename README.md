# OOP

### NYP'nin 4 Temel ilkesi

&emsp; Nesne yönelimli programlama dilinin nesne yöenlimli programlamayı uyguladığını anlamak için bu 4 temel ilkeyi sağlıyor olması gereklidir. Bu temel ilkeler kodların değiştirilebilirlik, yedinden kullanım ve esneklik gibi kriterlerin sağlanmasına ön ayak olurlar. Bu ilkeler;

- **Encapsulation (Kapsülleme)**
- **Ingeritance (Kalıtım)**
- **Polymorphism (Çok Biçimlilik)**
- **Abstraction (Soyutlama)**


------------


# Encapsulation (Kapsülleme)
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


## Encapsulation (Kapsülleme) Mantığı
&emsp;  Kitap adında bir sınıfımız olsun ve bu sınıfımıza ait 3 adet değişkenimiz olsun bunlar; `kitapAdi`, `sayfaSayisi` ve `yazar`. Bu değişkenlerin erişim belirleyicileri **public** olsun ve her sınıftan erişebilsin.

|<center>Kitap</center>|
| :------------ |
|- kitapAdi : string<br>- yazar : string<br>- sayfaSayisi : int|
|<br><br><br>|

&emsp;  Kitap sınıfından book adlı bir nesne oluşturalım ve bu nesnenin niteliklerini belirtelim. Peki biz bu sınıfa ait nitelikleri tanımlarken sayfa sayısını negatif bir değer girseydik ne olurdu? Hiç bir kitabın sayfa sayısı negatif bir değer olamayacağı için, nesnemizde bir anlamsızlık olacaktır.

|<center>Kitap : book</center>|
| :------------ |
|kitapAdi = "Harry Potter"<br>yazar = "J. K. Rowling"<br>sayfaSayisi = "-10"|
|<br><br><br>|

&emsp;  Biz bu sorunu constructor (kurucu) metoduna yazacağımız bir kontrol ile çözebiliriz. Ama sorunlarımız hala bitmedi, biz sınıfa ait niteklere hala dışarıdan erişebiliyoruz çünkü erişim belirleyici "**public**". Bu sorunu çözmek için sınıfa ait nitelikleri dışarıdan erişimi kapatmamız gerekir ve oluşturduğumuz niteliklerin erişim belirleyiclerini (Access Modifiers) değiştirmemiz gerekli. Tüm publicleri private olarak değiştiriyoruz.

|<center>Kitap</center>|
| :------------ |
| - kitapAdi : string<br>- yazar : string<br>- sayfaSayisi : int |
| + Kitap(kitapAdi,yazar,sayfaSayisi)<br><br><br> |

&emsp;  Sınıfa ait niteliklerin izinlerini **private** yaparak bu sorunu çözdük ama, biz book nesnesine ait değişkenlere erişimi tamamen kısıtladık. Yani biz oluşturduğumuz nesneye ait sayfa sayısını herhangi bir yerden çağıramayız çünkü değişken **private** olarak tanımlandı. Yada sayfa sayısı yanlış girilmiş bir nesneyi daha sonra **düzenleyemeyiz**. Bu sorunu çözmek için sınıfa ait değişkenlerimizi **kapsülleyerek**, sınıf içerisinde ki metotlar yardımı ile değişkenlerimizi koruma altına alıyoruz ve kullanıma sunuyoruz. Bu metotlara **Getter** ve **Setter** metotları diyoruz

|<center>Kitap</center>|
| :------------ |
| - kitapAdi : string<br>- yazar : string<br>- sayfaSayisi : int |
| + Kitap(kitapAdi,yazar,sayfaSayisi)<br> + getKitapAdi(): string<br> + setKitapAdi(String KitapAdi) : void<br> + getYazar() : string<br>+ setYazar() : void<br> + getSayfaSayisi() : int<br>+ setSayfaSayisi() : void  |







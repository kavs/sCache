sCache Class
=========

Kolay kullanımlı PHP dosya cache sistemi

- Sıkıştırma Özelliği
- Load hesaplama özelliği
- Belirlediğiniz sayfaları ön belleklemez ( options kısmına bakınız )
- Dosya uzantısı ve dizin belirleme olanağı 
- Hızlı entegrasyon özelliği sadece sınıfı çağırmak yeterli.


Youtube üzeri anlatım ( eski sürüm / old versiyon and turkish ) => **[sCache Kullanımı](https://www.youtube.com/watch?v=ti4p3LhLYzk)**

Redis Desteği ile kullanım =>  **[Döküman](https://github.com/saltun/sCache/tree/master/Redis)**


2 Adımda Kurulum
===========================

sCache sınıfını sayfamıza dahil edelim.

``` php
require_once "sCache.php";

```

Sayfamızın en üst kısmın'da sCache'i çalıştıralım.
**eğer sayfanın en üstünde çalıştırmaz iseniz cache tam anlamı ile çalışmaz**

``` php
$sCache = new sCache();
```

Tüm kurulum işlemi bu kadardır. 

> **Notlar:**

> - Eğer zaman değeri belirmez iseniz cache süreleri 60 saniyedir.
> - Eğer özel cache yolu belirtmez iseniz ana dizinde **sCache** dizin oluşturup içinde tutacaktır.
> - Cache adresleri md5 ile şifrelenip tutulmaktadır.
> - Eğer cache'e sıkıştırma özelliğini aktif etmez iseniz sıkıştırma yapmadan tutacaktır.
> - Eğer load özelliğini açmaz iseniz load değerleri gösterilmeyecektir.
Ayarları düzenlemek için dizi olarak ayarları göndermeniz gerekir bunu nasıl yapacağınızı öğrenmek için alttaki dökümana bakınız.




Ayarlar ( Options )
===========================
Ayarları bir dizi halinde sınıfın başlangıcında göndermeniz gerekir göndere bileceğiniz değerler ise altta listelenmiştir
- time = Cachenin tutulacağı süre değeri ( standart 60 saniye ) 
- dir = Cache dosyalarınızın tutulacağı dizin adı. Yok ise otomatik oluşturulur ( standart **sCache** ) 
- buffer = Oluşturulan cache dosyalarında sıkıştırılma yapılmasını ister iseniz **true** değerini göndermelisiniz ( standart kapalıdır ) 
- load = Sayfanın load süresi yani açılma süresinin en altta görünmesini istiyor iseniz **true** değeri göndermelisiniz.
- external = Cache harici sayfaları bir dizi olarak gönderir iseniz bu dosyalar cachelenmez.
Şimdi yukarıdaki özelliklerin hepsini kullanarak örnek bir ayar dizini oluşturup gönderelim.
- extension = Oluşturulacak cache dosyasının uzantısını belirleme olanağı sağlar eğer bir değer girmez iseniz standart olarak .html olarak oluşturacaktır.

``` php
$options = array(
	'time'   => 120, // 120 saniye yani 2 dakika
	'dir'    => 'sCache2', // sCache2 klasörü oluşturup buraya yazılsın.
	'buffer' => true, // html sayfalarımızın sıkıştırılmasını aktif edelim.
	'load'   => true,  // sayfamızın sonunda load değerimiz görünsün.
	'external'=>array('nocache.php','nocache2.php'), // Burada belirttiğiniz sayfalar ( dosyalar ) cachelenmez.,
	'extension' => ".scache", // standart değer .html olarak ayarlanmıştır cache dosyalarınızın uzantısını temsil etmektedir.
	);

$sCache = new sCache($options); // ayarları sınıfımıza gönderip sınıfı çalıştıralım.
```

Cache sistemini kapatma
===========================
Cache sisemini kapatmak isterseniz ayarlar değişkeninden sonra 2. değer olarak false değerini gönderir iseniz cache sistemi aktif olmayacaktır. (  example3.php)
``` php
$sCache = new sCache($options,false);
```


Tüm Cache dosyalarını temizleme
===========================
clearCache fonksiyonunu çalıştırdığınız zaman cache'de belirtilen dizindeki tüm cache dosyaları silinir eğer standart dizin dışında farklı bir dizinde cache dosyalarınızı tutuyor iseniz ayarları göndermeyi unutmayınız.
``` php
$sCache->clearCache();
```



Author : Savaş Can Altun
Mail : savascanaltun@gmail.com
Web : http://savascanaltun.com.tr

# Directory Traversal

Directory Traversal (Dizin Geçişi), Path Traversal ismi ile de bilinen saldırganın uygulamanın çalıştığı sunucu üzerinden dosya okumasını sağlayan zafiyettir. Uygulama kodları veya verileri, konfigürasyon dosyaları, kimlikler, hassas sunucu dosyaları gibi veriler bu yolla okunabilir. Bazı durumlarda saldırganın dosya yazma izni de olabilmektedir. Bu gibi durumlarda ise saldırgan uygulama verilerini değiştirebilir veya sunucuda tam yetkili olabilir.

![https://portswigger.net/web-security/file-path-traversal adresinden alınmıştır.](<../.gitbook/assets/image (2).png>)

Zafiyetin nasıl çalıştığını ve sömürüldüğünü görmek için bir alışveriş uygulamamızın olduğunu düşünelim. Bu uygulamada da ürün resimlerinin yüklendiğini varsayalım.

Ürün resimlerinin sunucu üzerindeki dosya yolu:

| **/var/www/images/218.png** |
| --------------------------- |

Uygulama ise bu resmi ekranda göstermek için aşağıdaki gibi bir kullanım yapar.

| **\<img src="/loadImage?filename=218.png"**  |
| -------------------------------------------- |

Eğer uygulama üzerinde kullanıcıdan gelen veriyi kontrol etmeden direk fonksiyonu çalıştırırsak, saldırgan bu giriş alanını manipüle edebilir.

Bilindiği gibi Linux dosya sisteminde bir üst dizine geçme komutu “../” dur. Saldırgan bu teknik ile aşağıdaki komutu çalıştırabilir.

| **https://website.com/loadImage?filename=../../../etc/passwd** |
| -------------------------------------------------------------- |

Bu isteği alan sunucu filename değişkenin aldığı değeri doğrudan çalıştırdığı için sunucu üzerindeki passwd dosyasının sonucunu saldırgana dönmüş olur. Birden fazla “../” ifadesinin kullanım sebebi en üst dizine “/” çıkıp, sonrasında /etc/passwd dosyasına erişim sağlamaktır.

#### Önlemler

Bu zafiyetten korunmanın iki temel yolu vardır.

* Uygulama üzerinde kullanıcıdan gelen veri kontrol edilmeli ve beyaz liste girdi denetimi yaklaşımı ile yalnızca istenen girdi türlerine izin verilmelidir. Örneğin sadece alfanümerik karakter olmasını bekliyorsak, bu karakter dizisinin dışında bir karakter gelmesi durumunda fonksiyon çalışmamalıdır. Böylece “../../../etc/passwd” gibi gelebilecek bir komut içerisinde özel karakterler barındırması sebebiyle çalışmayacaktır.
* Kullanıcıdan gelen veri kontrol edildikten sonra, kullanıcıdan gelen girdinin uygulamanın kök dizininde olup olmadığının kontrolü gereklidir. Eğer uygulama dışından bir dizin çağırılıyorsa çalışmayacaktır.&#x20;

Örnek kod:

| <p><strong>File file = new File(BASE_DIRECTORY, userInput);</strong></p><p><strong>if (file.getCanonicalPath().startsWith(BASE_DIRECTORY)) {</strong></p><p>    <strong>// process file</strong></p><p><strong>}</strong></p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

_NOT:_

Önlem olarak verdiğimiz çözüm uygulanmadığı ve kara liste yöntemi ile “../” gibi girdileri engelleyerek yapılan çözümler atlatılabildiği için, beyaz liste girdi denetimi uygulanması çok kritiktir.

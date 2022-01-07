# Giriş

Günümüz modern web uygulamalarında hemen her işlevde verilerin depolanması ve bu verilerin bilgisayar ağları içerisinde taşınması ihtiyacı bulunur. Verilerin işlenmesi için önemli noktalardan birisi de aynı veri formatının kullanılması açısından standart bir veri formatı oluşturulmasıdır. Bu veri formatlarının işlenmesi sırasında ise “insecure deserialization” zafiyetleri ortaya çıkabilir.

Insecure Deserialization zafiyetini incelemeden önce zafiyetin temelini oluşturan **“Serialization”** ve **“Deserialization”** kavramları hakkında bilgi sahibi olmamız gerekiyor.

## Serialization

Türkçe olarak “serileştirme” olarak adlandırabileceğimiz bu kavram, bazı nesneleri daha sonra geri yüklenebilecek bir veri biçimine dönüştürme işlemidir. Bu işlem sırasında nesneler “bytestream” yapılarına dönüştürülür. Uygulamalar, genellikle depolama veya iletişimin bir parçası olarak gönderilmek üzere nesneleri seri hale getirir.

Verileri seri hale getirilirken, nesnenin nitelikleri ve aldığı değerler kaydedilir.  “Ali Veli” adında 25 yaşında bir erkek, {male|25|Ali|Veli} gibi bir formata dönüşür.

Örneğin PHP’de aşağıdaki gibi bir kullanıcı nesnemiz olsun;

| <p><strong>$user->name = "carlos";</strong></p><p><strong>$user->isLoggedIn = true;</strong></p> |
| ------------------------------------------------------------------------------------------------ |

Bu nesne serileştirildiğinde aşağıdaki gibi görünür.

| **O:4:"User":2:{s:4:"name":s:6:"carlos"; s:10:"isLoggedIn":b:1;}** |
| ------------------------------------------------------------------ |

Bu veriyi aşağıdaki gibi yorumlayabiliriz.

* **O4:"User"** – 4 karakterli “User” isimli bir sınıfa ait bir nesne (object)
* **2** – nesneye ait olan iki nitelik olduğu belirtiliyor.
* **s:4:"name"** – İlk nitelikteki veriye ait key değerinin 4 karakter dizesi (string) "name" olduğu belirtiliyor.
* **s:6:"carlos"** – İlk nitelikteki veriye ait value değerinin 6 karakter dizesi (string) "carlos" olduğu belirtiliyor.
* **s:10:"isLoggedIn"** - İkinci nitelikteki veriye ait key değerinin 10 karakter dizesi (string) "isLoggedIn" olduğu belirtiliyor.
* **b:1** - İkinci nitelikteki veriye ait value değerinin “boolean true” olduğu belirtiliyor

## Deserialization

Türkçe olarak “seriden çıkarma” olarak adlandırabileceğimiz bu kavram, serileştirme işleminin tersidir, bir formattan yapılandırılmış verileri alır ve tekrar bir nesne olarak yeniden oluşturur. Bugün, verileri seri hale getirmek için en popüler veri formatı JSON'dur.

![https://portswigger.net/web-security/deserialization adresinden alınmıştır.](<../.gitbook/assets/image (7).png>)

Birçok programlama dili, nesneleri serileştirmek için kendi içerisinde bir yetenek sunar. Bu yerel biçimler, genellikle serileştirme sürecinin özelleştirilebilirliği de dahil olmak üzere JSON veya XML'den daha fazla özellik sunar.

![https://infosecwriteups.com/insecure-deserialization-its-super-hard-or-is-it-94d89e2847 adresinden alınmıştır.](<../.gitbook/assets/image (16).png>)

Ne yazık ki, bu yerel seriden çıkarma mekanizmalarının özellikleri, güvenilmeyen veriler üzerinde çalışırken kötü amaçlı etkilere olanak sağlayabilir. Seriden çıkarma sırasında, güvenilmeyen bir kaynaktan veri okuma, kullanıcı girdisini doğrulamadan geçirmeden işleme, dijital imzaları doğrulanmamış sınıflardan veri okuma gibi işlemler ile Insecure Deserialization zafiyeti ortaya çıkabilir. Insecure deserialization saldırıları, hizmet reddi (DoS), erişim denetimi ve uzaktan kod yürütme (RCE) gibi etkiler ortaya çıkarabilir. Deserialization saldırıları çoğunlukla tespit edilmesi zor ve sebep oldukları etki açısından büyük saldırılardır. Temelde kullanıcının gönderdiği özel hazırlanmış seri halindeki (serialized) verilerin seriden çıkarılması (deserialization) sırasında ortaya çıkan saldırılardır.

Serialization/Deserialization işlemleri ile karşılaşılabilecek bazı alanlar aşağıdaki gibidir;

* HTTP Parametreleri (ViewState), Cookie, Bileşenler
* XML
* JSON
* Veri tabanı, Mesaj Kuyrukları

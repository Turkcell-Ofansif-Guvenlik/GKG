# Güvenli Şifre Saklama

Şifrelerin güvenli olarak saklanması için, özet (hash) algoritmaları kullanılır. **Özet algoritmaları**, açık metni geri getirilemez şekilde, belirli uzunluktaki karakter dizilerine çeviren fonksiyonlardır.

![](<../.gitbook/assets/image (24).png>)

Özetlerin geri getirilemez olması sebebiyle kimlik doğrulama yapılan veri tabanının ele geçirilmesi durumunda dahi saldırganlar kullanıcı şifrelerini doğrudan göremezler. Ayrıca veri tabanına erişim yetkisi olan personelin de kullanıcı şifrelerini bilmemesi sağlanacaktır.

Özet algoritmaları sayesinde geri getirilemez bir şekilde saklanan şifrelerin de elde edilmesi için saldırganların yöntemleri vardır. Bunların başında **Rainbow tables** kullanımı gelir.

**Rainbow tables**, bir açık metin ve bu metinin özet algoritması sonucu çıktısını içeren **tablolardır**.

| **Açık Metin** | **MD5 Hash**                     |
| -------------- | -------------------------------- |
| test           | 098f6bcd4621d373cade4e832627b4f6 |
| 12345          | 827ccb0eea8a706c4c34a16891f84e7b |
| qwerty         | d8578edf8458ce06fbc5bb76a58c5ca4 |

Saldırgan özeti elde ettikten sonra bu tablolardaki değerleri karşılaştırarak, açık metinin ne olduğunu kolayca bulabilir. Tablonun tamamını oluşturmamış olsa dahi saldırgan özeti aldıktan sonra **kaba kuvvet** yöntemi ile açık metin oluşturabilir ve bu metni özet algoritmasından geçirerek doğru değeri arayabilir. Bu nedenle özet kullanımında da dikkat edilmesi gereken noktalar vardır.

Rainbow tables’da tüm olası karakter dizilerinin yer alması mümkün olmadığından en çok kullanılan şifreler ve özet değerleri bulunur. Bu nedenle basit ve varsayılan bırakılmış şifreler kullanılmamalıdır. MD5 gibi düşük güvenlikli olduğu kabul edilen özet algoritmaları kullanılmamalıdır. Bu algoritmaların tabloları internet üzerinde çok kolay erişilebilir.

Bir diğer alınması gereken önlem ise bu tablo saldırılarından etkilenmemek için özet elde edilirken mutlaka **tuzlama** **(salt)** kullanılmalıdır.

Eğer bir şifrenin özetini almak ve veri tabanı içerisinde güvenli bir şekilde saklamak istiyorsanız önerilen en iyi yöntem, “**\<GLOBAL\_SALT> + \<USER DEFINED PASSWORD> + \<USER SPECIFIC IDENTIFIER>**” toplamından oluşan metin değerinin özetinin alınarak veri tabanı üzerinde saklanmasıdır. Bu işlemde global salt kullanımının en büyük sebebi internet ortamında birçok metin değerinin özet değerinin zaten hesaplanmış olmasıdır. Özet değerleri geri döndürülemez değerlerdir ancak bir metnin özet değerini zaten bilirseniz metin değerini de elde etmişsiniz demektir.

Bu gibi metin/özet şeklinde tutulan tablolara rainbow table isimi verilmektedir. Bir özet değerinin metin değerini öğrenmek istediğinizde özet hesaplayarak sonrasında metin değerini öğrenmek istediğiniz özet ile karşılaştırmak gibi maliyetli bir işlem yapmaktan kaçınıp zaten hali hazırda hesaplanmış özet değerleri arasında sadece arama işlemi yapmanıza olanak sağlarlar.

Global salt kullanımı ile parola değerinin başına sadece kendinizin bildiği eşsiz bir değer (SALT) koyduğunuzda aslında salt+parola değerinin özetini aldığınız için bu gibi değerlerin rainbow table aracılığı ile bulunması çok zorlaşmaktadır. Yukarıda verilen yöntemde bulunan “user identifier” seçeneği isteğe bağlı olarak verilmiştir ancak en iyi uygulama pratiklerine örnektir.

# Simetrik – Asimetrik Şifreleme

Daha önce de değinildiği üzere şifreleme genel olarak simetrik ve asimetrik olarak ikiye ayrılmaktadır. Burada simetrik şifrelemeden kasıt yalnızca bir adet gizli anahtar içeren basit bir şifreleme türüdür. Asimetrik şifreleme için ise şifreleme ve şifre çözme işlemleri için farklı anahtarlar kullanılan bir şifreleme türüdür.

## Simetrik Şifreleme

Simetrik şifreleme en eski şifreleme yöntemlerinden biridir. Gönderici ve alıcı aynı gizli anahtar ile şifreleme ve şifre çözme işlemlerini yapmaktadır. Örnek olarak AES, DES, RC4, RC5 verilebilir.

![](<../.gitbook/assets/image (13).png>)

**Avantajları:**

* Şifreleme işlemleri asimetrik şifrelemeye göre çok daha hızlıdır.

**Dezavantajları:**

* Tek bir anahtar kullanıldığından manipülasyon ve veri sızıntısına daha açıktır, bütünlük sağlanamaz.
* Anahtar saklanması zordur, ölçeklenebilir değildir.
* Kimlik doğrulama yapılamaz, anahtara sahip herkes şifreleme yapabilir.

## Asimetrik Şifreleme

Asimetrik şifrelemede simetrik şifrelemeden farklı olarak şifreleme ve şifre çözme için farklı anahtarlar kullanılır. Göndericide ve alıcıda ikişer anahtar bulunur, gönderici şifrelerken alıcının açık anahtarını (public key) kullanırken alıcı kendi gizli anahtarı (secret key) ile şifreyi çözümleyebilir.

Gizli anahtar kişiye özeldir, açık anahtar ise herkese açıktır. Örnek olarak RSA, Diffie-Hellman, ECC verilebilir.

![](<../.gitbook/assets/image (12).png>)

**Avantajları:**

* Simetrik şifrelemeye göre daha güvenlidir, anahtarın çalınma ihtimali düşüktür.
* İmzalama ve kimlik doğrulama yapılmaktadır.
* Anahtar saklamak daha kolaydır, gizli anahtarlarla anlık olarak açık anahtar oluşturulabilir.

**Dezavantajları:**

* Simetrik şifrelemeye nazaran daha yavaş bir şifreleme türüdür.
* Daha fazla işlem gücü (CPU) gerektirir.

\


&#x20;****&#x20;

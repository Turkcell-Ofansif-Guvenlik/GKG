# Giriş

Güvenli tasarım için her zaman gereksiz girdi alanını azaltmak, sistemi sürekli taramak veya güncelleştirme almak yeterli kalmayabilir. Hata durumunda fırlatılan bir bilgi, riskli HTTP metotlarının kullanımı veya eksik-hatalı bir güvenlik başlık bilgisi kötü sonuçlar doğurabilmektedir.

Saldırganlar genellikle güvenlik yamaları eksik olan sistemler, varsayılan kullanıcı adı - şifre bırakılmış sayfalar, kullanılmayan ya da korumasız dosya ve klasörler aracılığı ile sistem hakkında bilgiler alır ve yetkisiz erişimlerini sağlarlar.

Hatalı güvenlik ayarları uygulamanın her seviyesinde olabilir, ağ katmanından, veri tabanına kadar her seviyede bu hatalı ayarlar olabilir. Otomatik tarama araçları tarafından da kolayca tespit edilebilmesi sebebiyle canlı sistemler için büyük risk içermektedir.

Bu güvenlik zafiyetlerini gidermek için öncelikle kullanılmayan tüm özellik, dosya, klasör, port, bileşen vb. sistemden kaldırılmalıdır. Kullanılanların ise envanteri tutulmalı, düzenli olarak güncellemeleri yapılmalıdır. Düzenli olarak otomatik taramaların yapılması da gözden kaçacak zafiyetlerin tespit edilmesini sağlayacaktır. Varsayılan kullanıcı adı ve şifreler de kurulum anında kaldırılmalı, kullanılmamalıdır.

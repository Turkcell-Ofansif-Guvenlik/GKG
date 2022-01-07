# HTTP Güvenlik Başlık Bilgileri

Başlıklar bilindiği üzere http protokolünün hem istek hem de yanıtlarında bulunan ve içeriğin meta bilgilerini taşıyan kısımlardır. Güvenlik başlıkları istemci tarafında güvenlik önlemlerini aktifleştiren, istemcinin davranışlarını değiştirebilen HTTP yanıt başlıklarıdır.

&#x20;

**X-Frame-Options:** Web sitelerinde **Clickjacking** güvenlik açığını önlemek için X-Frame-Options başlığı kullanılır. Bu başlığı uygulayarak, tarayıcıya web sayfasının çerçeve/iframe içine yerleştirmemesi söylenir. Bunun tarayıcı desteğinde bazı sınırlamaları vardır, bu yüzden uygulamadan önce kontrol edilmelidir. Bu başlık bilgisinin alabileceği 3 adet farklı değer vardır.

* **DENY**, başlık bilgisi web sitesinin iframe ya da benzeri bir yöntem ile embed edilmesine asla izin vermez.
* **SAMEORIGIN**, web sitesinin yalnızca protokol + host + port olarak eşleştiği bir site tarafından embed edilmesine izin verir. (Önemli olan temel şemadır örneğin https://example.com/index sitesi https://example.com sitesine izin verirken https://example.com:85/index veya http://example.com sitesine izin vermeyecektir.)
* **ALLOW-FROM**, Yalnızca belirtilen URL tarafından embed edilebileceği anlamına gelmektedir.

**Strict-Transport-Security:** HTTP Strict-Transport-Security (HSTS) kullanıcının istemci tarafından yaptığı her istek için kullanıcıyı HTTPS kullanmaya zorlamaktadır. Kullanıcı daha öncesinde sunucudan bu başlık bilgisini bir kere aldığında sunucuya bir sonraki istekleri HTTPS olarak yapacaktır. MITM ve downgrade saldırılarının önüne geçmek için geliştirilmiştir.

**X-Content-Type-Options:** Tarayıcılar belirtilmediği sürece göstereceği dosyanın içeriğini belirlemeye çalışmaktadır (MIME Type sniffing). Bu başlık bilgisini gönderen sunucu bu başlık bilgisi altında nosniff göndererek tarayıcının içerik üzerinde karar vermesini engellemelidir. Kullanılmadığı taktirde depolanmış XSS zafiyetlerine neden olabilir. Örneğin; uzantısı .jpg ama içeriği HTML olan bir dosya yükleme modülündeki korumalar aşılıp sunucu tarafına yüklenebilirse URL üzerinden .jpg uzantılı dosya istendiğinde HTML olarak yorumlanacaktır ve bu durumda depolanmış XSS zafiyeti oluşacaktır.

**HttpOnly ve Secure Bayrakları:** Web uygulamaları kullanıcıların oturumlarını oturum kimlikleri üzerinden takip eder. Oturum kimlikleri kullanıcıya **HTTP-Set-Cookie** başlık bilgisi ile birlikte verilir. Tarayıcıda kullanıcı her talep yaptığında oturumun açık kalması için bu bilgiyi isteğe eklemektedir. HTTPOnly bayrağı, oturum anahtarı bilgisine, “istemci taraflı programlama ile ulaşılmamalıdır” ilkesi göz önünde bulundurularak geliştirilmiştir. HTTPOnly bayrağı gören tarayıcı document.cookie üzerinden çerezlere erişim sağlanmaya çalıştığında HTTPOnly bayrağı olan değerleri işleme sokmamaktadır. Secure bayrağı ise, çerezin sadece güvenli bağlantılar üzerinden taşınmasını garanti altına alır.

# Önlemler

CSRF zafiyeti, daha önce de bahsettiğimiz gibi tarayıcıların çerez ekleme davranışından kaynaklı olarak ortaya çıkmaktadır. Tarayıcılar, başka bir kaynaktan tetiklenen isteklere çerez bilgisini dahil ediyor ve isteği alan uygulama sunucusu bu isteğin kendisi üzerinden mi yoksa başka bir kaynaktan mı yapıldığını kontrol etmeden işleme aldığı için zafiyet oluşuyor.

* İlk olarak, HTTP GET metodu üzerinden durum değişikliğine sebep olacak bir işlem yapılmaması gerekmektedir.
* Sunucu tarafında, gelen isteklerin kendi üzerinden mi yoksa başka bir kaynaktan mı yapıldığını kontrol etmek için de CSRF Token kullanılması gerekir. Kullanıcının oturumu ile ilişkili bir CSRF token üreterek, cevapta “hidden” alan olarak dönülür. Ardından kullanıcının yapacağı isteklerde CSRF token bilgisi de gönderileceği için sunucu tarafında, CSRF token’ın kontrolü sağlanarak, çözüm sağlanabilir.

| **\<input type="hidden" name="csrf-token" value="CIwNZNlR4Xbis6s3Hy9aZr51JF39I8yWnWX9wX4WFoz" />** |
| -------------------------------------------------------------------------------------------------- |

Örnek senaryoda saldırgan formu hazırlayıp, kullanıcının oturumu açık iken bir şekilde tetiklenmesini sağlasa da çerez bilgisi tarayıcı tarafından yine eklenecek fakat CSRF token saldırgan tarafından bilinmediği için isteği karşılayan uygulama sunucusu isteği reddedecektir. **CSRF Tokenlar**, oturum başına **benzersiz**, **tahmin edilemez** ve **karmaşık** olmalıdır. Kullandığınız framework’ün sunduğu CSRF koruma yapılarının kullanılması önerilir. Örneğin,

**.NET için Antiforgery token** - [https://docs.microsoft.com/en-us/aspnet/core/security/anti-request-forgery?view=aspnetcore-2.1](https://docs.microsoft.com/en-us/aspnet/core/security/anti-request-forgery?view=aspnetcore-2.1)

**Spring için** - [https://docs.spring.io/spring-security/site/docs/5.0.x/reference/html/csrf.html](https://docs.spring.io/spring-security/site/docs/5.0.x/reference/html/csrf.html)

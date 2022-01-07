# Saldırılara Genel Bakış

Saldırganların, saldırdıkları noktalar aslında "normal" bir kullanıcının sürekli kullandığı noktalardan farklı değildir.

Kullanabilmemiz için kimlik doğrulama yapmamız gereken bir uygulama olsun. Burada "normal" kullanıcılar uygulamayı kullanabilmek için öncelikle giriş yapmalıdır. Bu giriş işleminde kullanıcı, **kullanıcı adı ve parolasını** girer ve sunucuya kimliğinin doğrulanması için gönderir.

![https://secure-bits.org/sicheres-passwort-was-macht-ein-passwort-sicher/ adresinden alınmıştır.](<../.gitbook/assets/image (34).png>)

Arka planda istemciden sunucuya gönderilen "**RAW HTTP**" paketlerini son kullanıcı genelde bilmez ve görmez. Ancak uygulama üzerinde yapılan işlemler arkadaki sunucuya bir istek gönderir ve bu istek sunucuda işlenir. Sunucu tarafına gönderilen paket içerisindeki girdilere "**parametre**" denir.

![](<../.gitbook/assets/image (11).png>)

Paket içerisindeki parametrelere saldırganlar "**beklenenin dışında**" bilgiler göndererek sunucunun **amaçlanan dışında** çalışmasını sağlar.

## Girdi Noktaları

Girdi noktaları, kullanıcı tarafından yaptığı işlem ile oluşturulmuş ve bu işleme yönelik sunucudan bilgi gelmesini sağlayan **parametrelerdir**. Örnek olarak kullanıcı adı-şifre doğrulaması yapan bir kullanıcı parametre olarak bu iki değeri gönderir ve sunucu bu işlemi yapar, doğru ya da yanlış olmasına göre farklı bilgileri geri kullanıcıya döner.

Girdi noktalarını **tarayıcıların geliştirici araçları** üzerinden de görebiliriz. Ancak saldırganlar ve güvenlik araştırmacıları buradan paketlerin tek tek görmek yerine "**Web Application Proxy**" kullanmayı tercih ederler.

En çok kullanılan iki proxy olarak [OWASP ZAP](https://owasp.org/www-project-zap) ve [Burp Suite](https://portswigger.net/burp) verilebilir. Doküman içerisindeki bazı bölümlerde "**Burp Proxy**" kullanılan örnekler yer almaktadır.

Bir giriş işlemi sırasında gönderilen parametreler **yalnızca kullanıcı adı ve şifre değildir**. HTTP **başlık bilgileri**, **istek gövdesi** ve **URL** de dahil olmak üzere birçok bilgi sunucuda işleme alındığından bu alanların da parametre olarak düşünülmesi gerekir.

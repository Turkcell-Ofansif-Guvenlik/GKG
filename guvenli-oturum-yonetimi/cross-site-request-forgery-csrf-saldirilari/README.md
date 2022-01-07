# Cross Site Request Forgery (CSRF) Saldırıları

HTTP (Hypertext Transfer Protocol), durum bilgisi tutmayan (stateless) bir protokoldü. Yani bu durumda bir istek ve cevap döngüsü yaşandıktan sonra ve ikinci bir istekte, bir önceki döngüde ne olup bittiğine dair herhangi bir bilgi tutulmamasına neden olmaktadır.

HTTP protokolü ilk başlarda sadece statik sayfalar sunmak için tasarlanmıştı. Web teknolojilerinin gelişmesiyle birlikte uygulamalar dinamik ve daha karmaşık yapılar haline geldi. Bu gelişmeyle birlikte web uygulamaları üzerinde işlem yapan kullanıcıları tanıma ve onlara uygun içerikler sunma ihtiyacı ortaya çıktı.

Çerezler de işte tam bu noktada hayatımıza girdi. Yapılan her istekte kullanıcı adı ve parola bilgisi gönderilmeden çerezler üzerinden işlem yapan kullanıcı bilgisi, sunucu tarafında takip edilebilir duruma geldi.

![](<../../.gitbook/assets/image (8).png>)

Resmi inceleyelim, resimdeki istemciyi kullanıcının tarayıcısı olarak düşünebiliriz.

1. İlk adımda, kullanıcı example.com adresine kullanıcı bilgileri ile giriş yapar.
2. İkinci adımda, sunucu tarafında kullanıcı bilgileri kontrol edilir ve doğru ise kullanıcı için bir oturum (session) oluşturularak, bu oturuma referans eden kimlik bilgisi “Set-Cookie” başlık bilgisi üzerinden tarayıcıya kaydedilir. Tarayıcı bu bilgiyi kendi içerisindeki veri tabanında saklar.
3. Oturumu açık olan kullanıcı örnek olarak profil sayfasını görüntülemek istediğinde tarayıcı tarafından çerez bilgisi de HTTP isteğine otomatik olarak eklenir ve bu isteği karşılayan web uygulaması, çerez üzerinden kullanıcının kim olduğunu bildiği için isteği onun oturumunda işletir.

Tarayıcı kendi üzerine kaydettiği çerez bilgisini bundan sonra kaydettirilen domaine yapılan isteklere otomatik olarak dahil eder. Tarayıcıların bu davranışı kötüye kullanılarak CSRF (Cross-site Request Forgery) adı verilen güvenlik açığının oluşmasına zemin hazırlamaktadır.

Siteler arası istek sahteciliği anlamına gelen CSRF zafiyeti, tarayıcının çerez ekleme davranışını kötüye kullanan bir güvenlik açığıdır.&#x20;

![https://medium.com/tresorit-engineering/modern-csrf-mitigation-in-single-page-applications-695bcb538eec adresinden alınmıştır.](<../../.gitbook/assets/image (14).png>)

Örnek olarak resimde yer alan kullanıcı, hesap bilgileri ile bankacılık uygulamasına giriş yapmış ve bankacılık uygulaması, kullanıcının tarayıcısına çerez bilgisini kaydetmiştir (1-2).

Ardından, kullanıcının oturumu aktif iken yan sekmede saldırgan tarafından hazırlanan (evil.com) -masum görünen- bir sayfayı ziyaret ettiğini düşünelim (3).

Saldırgan, kendi kontrolünde olan evil.com’un kaynak koduna bankacılık uygulamasında para transferini tetikleyecek olan formu hazırlayıp, eklemiş olsun. Oturumu açık olan kullanıcı her şeyden habersiz bir şekilde evil.com’u ziyaret ederek, saldırgan tarafından hazırlanan bu formu farkında olmadan otomatik olarak tetikleyecektir. İstek kullanıcının tarayıcısından çıkacağı ve tarayıcı da bankacılık uygulamasına yapılacak isteklere otomatik olarak çerez bilgisini dahil edeceği için günün sonunda yapılan istek, kullanıcının oturumunda işletilmiş olacaktır (4-5-6). Saldırgan bu durumu sömürerek, kurban kullanıcı üzerinden kendi hesabına para gönderebilecektir.

CSRF zafiyeti ile kullanıcının oturumunun aktif olduğu uygulama üzerinde bilgisi dahilinde olmayan işlemler tetiklenebilir. Bu zafiyet, görüldüğü yere göre kritik etkilere sebep olabilir. Örneğin, yönetici yetkilerinde kullanıcı oluşturabilme veya kullanıcı bilgilerinin değiştirilebilmesi gibi durumlarda bu zafiyetin etkisi artacaktır.

Bir diğer örnek olarak, kurban kullanıcı vulnerable.com’a giriş yapmış ve mail adresini ‘test@test.com’ olarak değiştirme işlemi yapıyor.

**Yapılan HTTP isteği;**

| <p>POST /email-change HTTP/1.1</p><p><strong>Host: vulnerable.com</strong></p><p><strong>Cookie: session=BxM87QxxMnKkQkVm4IwbMPaejwrxT6y1</strong></p><p>Accept-Encoding: gzip, deflate</p><p>Content-Type: application/x-www-form-urlencoded</p><p>Content-Length: 21</p><p>Connection: close</p><p> </p><p><strong>email=test%40test.com</strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Saldırgan, kendi kontrolünde olan bir sayfaya vulnerable.com üzerinde mail adresi değiştirme işlemini tetikleyecek formu hazırlayıp, ekliyor.

Saldırganın kontrolünde olan sayfanın kaynak kodu:

| <p><strong>&#x3C;html>&#x3C;body></strong></p><p>  <strong>&#x3C;form action="https://vulnerable.com/email-change" method="POST"></strong></p><p>    <strong>&#x3C;input type="hidden" name="email" value="hacker@hacker.com" /></strong></p><p>  <strong>&#x3C;/form></strong></p><p>  <strong>&#x3C;script></strong></p><p>    <strong>document.forms[0].submit();</strong></p><p>  <strong>&#x3C;/script></strong></p><p><strong>&#x3C;/body>&#x3C;/html></strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Form’un hedefi olarak, vulnerable.com adresinin /email-change yolu ve girdi değeri olarak ‘hacker@hacker.com’ mail adresi yazılmış. Saldırgan bir şekilde hedeflediği kullanıcının oturumu aktif iken kendi hazırladığı sayfayı ziyaret etmesini sağlayabilirse, kullanıcının tarayıcısı bu isteği vulnerable.com’a yaparken çerez bilgisini de dahil edeceği için bu istek kullanıcının oturumunda işleme alınacak. Böylelikle saldırgan hedeflediği kişinin mail adresini kendi belirlediği bir mail adresi ile değiştirebilmiş olacaktır. Ardından parolamı unuttum akışı üzerinden -parola sıfırlama bağlantısı saldırgan kontrolünde olan mail adresine geleceği için- hesabı ele geçirebilir.

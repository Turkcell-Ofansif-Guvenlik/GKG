# Giriş

HTTP protokolü durum bilgisi tutmayan bir protokoldür. Bu nedenle durum bilgisi genellikle **oturum kimlikleri** ile tutulur. Oturum yönetimi genellikle **HTTP Cookie başlık bilgisi** ile gerçekleştirilir ve çerezler durum bilgisini tutan oturum kimliklerini taşır.

Çerezler isim ve değer ikililerinden oluşurlar.

| **Çerez\_adı = Çerez\_değeri** |
| ------------------------------ |

Çerezlerin özellikleri **öznitelikler ile** tarafından belirlenir. **Domain** ve **Path**, **Expires** ve **Max-Age** ya da **Secure**, **HttpOnly** ve **SameSite** gibi öznitelikler ile çeşitli durumlarda ayarlanabilir.

Oturum yönetiminde kullanıcı kimlik bilgilerini sunucuya göndererek giriş yapmak ister. Sunucu üzerinde kontrol edilen kimlik bilgileri doğru ise sunucu, kullanıcının işlemlerini gerçekleştirebilmesi için, kullanıcının yetkileri ile bir oturum oluşturur ve bu oturumu tutan çerez değerini kullanabilmesi için kullanıcıya gönderir.

![https://docs.microsoft.com/tr-tr/aspnet/web-api/overview/advanced/http-cookies adresinden alınmıştır.](<../.gitbook/assets/image (9).png>)

Kullanıcı sunucu tarafından bildirilen oturum kimliği ile isteklerini yaparak yetkisi olan işlemleri yapabilir. Bu nedenle tahmin edilebilir çerez değerleri kullanılmamalı, çerez değeri kaba kuvvet ile tahmin edilemeyecek kadar güçlü, uzun ve karmaşık olmalıdır.

Oturum yönetiminin güvenliğini sağlamak için, kimlik doğrulama ve çıkış sayfaları da dahil olmak üzere tüm uygulama trafiği **SSL** ile gerçekleştirilmelidir. Uygulama içerisinde SSL olmayan içerik bulundurulmamalıdır. Hassas uygulamalarda SSL olmayan portlara cevap verilmemeli, bu portlar üzerinden hizmet sağlanmamalıdır.

Oturum çerezleri mutlaka Secure ve HttpOnly öznitelikleri ile işaretlenmelidir. Çerezin **Secure** olarak işaretlenmesi, çerez değerlerinin yalnızca SSL bağlantısı ile gönderilebileceğini belirtir. Bu sayede şifresiz trafik aracılığıyla çerezin çalışma ihtimali azaltılmış olacaktır. **HttpOnly** ile işaretlenmiş çerez ise yalnızca HTTP üzerinden erişilebilecektir. Bu sayede XSS saldırıları gibi durumlarda çerez değerinin Javascript ile saldırgan tarafından elde edilmesi ihtimali azaltılmış olacaktır.

Her kimlik doğrulama sonrasında oturum çerezi yenilenmeli, aynı çerez değeri kullanılmamalıdır. Benzer şekilde uygulamadan çıkış yapan kullanıcının da çerez değeri sonlandırılmalı, bu çerez ile tekrar oturuma erişilememelidir.

Uygulamanın amacına, niteliğine ve kullanıcı profiline göre **mutlak zaman aşımı** ve **inaktif zaman aşımı** belirlenmelidir. Bu süreleri dolduran çerezler de sonlandırılmalı ve oturuma erişim için izin verilmemelidir.

**Mutlak zaman aşımı** çerezin en uzun ne kadar süre geçerli olacağını gösterir. Kullanıcı aktif kullanıyor dahi olsa bu süre sonunda tekrar kimlik doğrulama yapılması istenir. Bu sayede herhangi bir yolla çerez değeri elde edilmiş olsa dahi saldırganların kullanıcı kaynaklarına erişimleri bir yerden sonra kesilebilir.

**İnaktif zaman aşımı** uygulama üzerinde belirli bir süre hiç işlem yapılmaması durumunda olan zaman aşımıdır. Yine bu süre sonunda kullanıcın çerez değeri sonlandırılmalıdır.

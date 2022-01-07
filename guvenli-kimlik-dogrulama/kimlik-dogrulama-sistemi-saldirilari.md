# Kimlik Doğrulama Sistemi Saldırıları

Kimlik doğrulama sistemlerindeki en önemli zafiyetlerden birisi art arda yapılan istekler ile kimlik bilgileri doğruluğunun sınanmasıdır. Otomatize edilerek yapılan bu tür saldırılara **kaba kuvvet saldırıları (Brute Force)** denilmektedir.

Saldırganların deneyebileceği milyonlarca kullanıcı adı - şifre çifti kombinasyonu vardır. Bunları **varsayılan yönetici hesabı** ele geçirme ya da kaba kuvvet saldırıları gibi yöntemleri uygulamak için kullanabilirler.

Saldırganların bir sistemi ele geçirmesi için bazen sadece bir yönetici hesabını ele geçirmesi bile yeterli olabileceği gibi ele geçirilen hesap ve uygulamanın amacına bağlı olarak saldırganlar bu hesapları aracılığıyla **para aklama, kimlik hırsızlığı ya da bilgi ifşası için kullanabilirler**.

Uygulama, kaba kuvvet gibi otomatik araçlar ile kimlik doğrulama saldırılarına izin veriyorsa, oturum bilgilerini URL’de gönderiyorsa ve oturum için kullanılan token değerlerini belirli bir süre sonra inaktif hale getirilmemesi sonucunda **broken authentication** zafiyetinden etkilenir.

## **Kimlik Doğrulama Saldırıları Engellenmesi**

Bu saldırıları engellemenin birkaç yolu bulunmaktadır. Bunlar arasında **çoklu kimlik doğrulama** **(multi factor authentication)** en sık kullanılan yöntemlerden birisidir. **Çoklu kimlik doğrulama yönteminde** kullanıcıdan alınan kullanıcı adı - şifre kombinasyonunun doğru olması durumunda sistem tarafından bir diğer tek kullanımlık parola istenmektedir. Bu parola genellikle SMS ya da e-mail gibi kullanıcı tarafından sahip olunan bir iletişim yöntemi ile tekrar doğru kişi olduğunu doğrulaması için gönderilen geçici bir karakter dizisidir. Genellikle kullanıcı adı - şifre doğru olduktan sonra yalnızca bir kez bu doğrulamanın yapılması kullanıcı deneyimi açısından daha iyi olduğundan **iki faktörlü doğrulama** **(two factor authentication)** da denilmektedir.

Bir diğer önlem ise **varsayılan kullanıcı adı ve şifrelerin** sistemlerde bulundurulmamasıdır. Özellikle uygulamanın varsayılan kullanıcıları için belirlenmiş şifreler internet üzerinden kolayca bulunabilen şifreler olduğu için her sistem kurulurken bu kullanıcılar kaldırılmalı, kaldırılamıyorsa kullanıcı adları ve şifreleri değiştirilmelidir.

Kimlik doğrulama işlemi mutlaka **sunucu tarafınd**a yapılmalı, trafik **TLS** ile iletilmelidir.

Kimlik doğrulama sürecinde yapılan **başarılı ve başarısız denemeler kayıt altına alınmalıdır**.

Framework tarafından sağlanan güvenilirliği bilinen kimlik doğrulama API’ları kullanılmalıdır.

Kullanıcı adı ve şifreler **kesinlikle kaynak kod içerisine konulmamalıdır**.

**Şifremi unuttum** akışlarının güvenliğine özen gösterilmelidir. Şifremi sıfırlama linki gönderiliyor ise bu linkin belirli bir süre geçerli olması sağlanmalıdır. Mümkünse OTP veya telefon kullanarak şifre sıfırlama yöntemi tercih edilmelidir.

Sunucu tarafında güvenli, yeterince uzun ve yeterince rastgelelik içeren bir oturum değerinin üretimi sağlanmalı, idle olma ve oturum kapatmış olma durumunda bu oturum değeri sonlandırılmış olmalıdır.

Burada dikkat edilmesi gereken nokta; Oturum değerlerinin sadece kullanıcı çerezlerinden kaldırılması asla yeterli değildir. Oturumun sunucu tarafında da sonlandırılması şarttır.

Oturum bilgisinin URL’de gönderilmesi sunucu erişim günlüklerinde ve tarayıcı geçmişinde kalacağı için tehlikeli olabilir. Bu nedenle oturum taşıyan değerlerin URL üzerinden paylaşılmaması gerekir.

Şifre tahmini saldırılarına karşı tüm kullanıcıların güçlü şifre kullanması zorlanmalıdır. Genel olarak güçlü şifreler için aşağıdaki maddelere uyması beklenir.

* En az 8 karakter uzunluğunda olmalıdır.
* Alfanümerik ve noktalama işaretleri içermelidir.
* Sıralı sayı ve harflere izin verilmemeli, kullanıcı adının şifrede kullanılması engellenmelidir.
* Geçmişte kullanılan 3 parola olmamalıdır.
* Belirli aralıklarla şifre değiştirmeye zorlanmalıdır.
* Şifrelerin güvenli bir şekilde saklanması **gerekmektedir**.

### Captcha Doğrulama

Tüm güvenlik önlemlerinin yanında mutlaka kullanılması gereken, resim doğrulamaya dayalı, otomatize araçlar ile insanı ayırt etmek için kullanılan [Turing testidir](https://tr.wikipedia.org/wiki/Turing\_testi). Makina tarafından çözülemeyecek bir resim içerisindeki verilerin kullanıcı tarafından girilerek insan olduğunu doğrulamasına, bu sayede otomatik araçlar tarafından işlemin taklit edilememesini amaçlar.

![](<../.gitbook/assets/image (27).png>)

Kimlik doğrulama aşamasında kullanılması durumunda öncelikle captcha’nın değeri kontrol edilmeli, bu değer yanlışsa kullanıcı adı - şifre doğruluğu kontrol edilmeden yeni captcha ile işlemin tekrarlanması istenmelidir.&#x20;

Kimlik doğrulama aşamasının yanı sıra yeni kullanıcı oluşturma, şifre sıfırlama isteği, kullanıcı silme, yorum yazma gibi alanlarda da kullanılmalıdır.

Captchaların sistemde kullanımı sırasında dikkat edilmesi gereken güvenlik önlemleri vardır. Doğru entegre edilmemiş bir captcha otomatize araçlara karşı güvenlik sağlamadığı gibi yanlış güvenlik hissiyatı da doğurabilir.

#### Captcha Zafiyetleri

Kırılması kolay captcha kullanımı, captcha’ların resim işleme ile kırılmasını bu sayede otomatik araçlar tarafından insan / robot kontrolünün atlatılmasına neden olabilir. Captcha’nın resim işleme ile kırılmasını engellemek için farklı fontlarda ve biçimi bozulmuş şekilde oluşturulması, arka planda gürültü içermesi, sadece harf ya da rakam gibi dar bir karakter seti ile oluşturulmaması gerekmektedir.

Captcha korumasının atlatılmasının bir diğer nedeni ise aynı captcha değerinin tekrar kullanılmasından kaynaklanan **Captcha Replay** saldırılarıdır. Bu teknik ile saldırgan bir captcha değerini manuel olarak doğru girer ve sunucu tarafından kabul edildiğini doğrular. Daha sonrasında aynı captcha değeri ve captcha kimliği ile isteği yenilediğinde işlem başarılı yanıt veriyorsa aynı captcha’yı kullanarak saldırılarına devam edebilir.

![](<../.gitbook/assets/image (5).png>)

Saldırgan örnekteki istekte daha sonra **captcha** ve **captchaHash** değerlerini sabit tutarak kullanıcı adı ve şifre alanlarını değiştirerek otomatik olarak parola kırma denemeleri gerçekleştirebilir.

Captcha Replay saldırılarının gerçekleştirilebilmesinin temel nedeni, girilen captcha değerinin oturumdan silinmemesidir. Doğru ve yanlış her denemeden sonra capthca ve hash değeri silinmeli, geçerliliği iptal edilmelidir. Örnek kod aşağıda verilmiştir.

| <p><strong>String captcha = request.getParameter(“captcha”);</strong></p><p><strong>c = (Captcha) session.getAttribute(Captcha.NAME);</strong></p><p> <strong></strong> </p><p><strong>//captcha değeri işlem doğrulauğuna bakılmaksızın oturumdan silinir. Böylece tek kullanımlık değer olur.</strong></p><p><strong>session.setAttribute(Captcha.Name, null);</strong></p><p> <strong></strong> </p><p><strong>if (c != null &#x26;&#x26; c.isCorrect(captcha)){</strong></p><p>     <strong>// doğru resim</strong></p><p><strong>}</strong></p><p><strong>else {</strong></p><p>     <strong>// yanlış resim</strong></p><p><strong>}</strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

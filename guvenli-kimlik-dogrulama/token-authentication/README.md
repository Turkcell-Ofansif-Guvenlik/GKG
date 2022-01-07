# Token Authentication

Token authentication yönteminde kullanıcı kimlik sunucusuna giriş bilgileri ile başarılı bir şekilde oturum açtığında kimlik sunucusu kullanıcıya tekil bir access token verir. Kullanıcı almış olduğu access token **geçerli olduğu sürece** oturumu üzerinde işlemler yapabilir. Kullanıcı oturumunu sonlandırmak istediğinde access token inaktif duruma çekilir ve bu token ile bir daha işlem yapılamaz. Aynı zamanda tokenlar, belirli bir süre kullanılmadığında (idle durum) inaktif duruma çekilmelidir. Basic authentication yapısından farklı olarak her istekte kullanıcı adı ve parola bilgilerini göndermek yerine işlemler tekil access tokenlar ile işlem yapılır. Tekrar token almak için ise kullanıcı yeniden giriş yapar. Jenerik bir token authentication akış diyagramı aşağıdaki gibidir.

![](<../../.gitbook/assets/image (10).png>)

Token authentication yapıları özellikle API çağrıları için ideal kimliklendirme ve yetkilendirme süreçleri sağlar. Kimliklendirme ve yetkilendirme süreçlerinde daha esnek bir yapı sağlar. Basic authentication yönteminde bulunan oturum sonlandırma eksikliği de bu yapı ile giderilmiştir.

Modern teknolojilerle birlikte farklı ihtiyaçlar ile birlikte jenerik token authentication yapılarına ek olarak farklı token yapıları kullanılmaktadır.&#x20;

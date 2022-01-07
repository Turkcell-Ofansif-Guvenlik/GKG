# Basic Authentication

En çok desteklenen, standart bir [metoddur](https://www.ietf.org/rfc/rfc2617.txt). Kullanıcı adı - şifre bilgisi HTTP isteğinde **Authorization** başlık bilgisi ile **base64** kodlanmış olarak gönderilmektedir. Sunucu bu başlık ile kimlik doğrulama yapar.

![https://docs.microsoft.com/tr-tr/aspnet/web-api/overview/security/basic-authentication adresinden alınmıştır.](<../.gitbook/assets/image (40).png>)

Burada dikkat edilmesi gereken nokta base64 bir **kodlama (encoding)** yöntemidir, **şifreleme (encryption) değildir**. [Internet siteleri](https://www.base64decode.org) ve çeşitli araçlar üzerinden de base64 kodlama kolayca geri çevrilebilmektedir. Örnek olarak yukarıdaki kimlik doğrulama için kullanılan base64 metni çözersek, kullanıcı adı - şifrenin **alice:password** olduğu görülecektir. Her HTTP paketinde tekrar gönderilmesi gerektiğinden **oturum yönetimi eksikliğine** sebep olur ve bu nedenle **kullanılması tavsiye edilmez**. Ancak kullanılması gereken zorunlu durumlarda da kullanıcı kimlik bilgilerinin şifreli transfer edilebilmesi için **TLS ile kullanılması gerekmektedir**. Yine her HTTP paketinde tekrar gönderilmesi gerektiğinden dolayı bir oturum bulunmamakta, dolayısı ile **oturum sonlandırma eksikliği** bulunmaktadır.

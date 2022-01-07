# Insecure Deserialization Zafiyetinin Sömürülmesi

## Nasıl Oluşur?

Java ile yazılmış bir uygulamaya yönelik senaryo üzerinden zafiyeti daha detaylı inceleyelim.

Uygulamamızda kullanıcıları tanımlayan sınıfımız aşağıdaki gibi olsun.

![Kullanıcı adı ve şifre özniteliklerini içeren “User” sınıfı](<../.gitbook/assets/image (37).png>)

Kullanıcı sınıfından bir nesne üretip bunu user.txt içerisine yazalım.

![Kullanıcı nesnesini dosya içerisine serileştirme](<../.gitbook/assets/image (6).png>)

Bytestream verisini user.txt dosyasından okuyalım ve kullanıcı sınıfını tekrar oluşturmak için deserialization yapalım.

![Kullanıcı nesnesinin dosyadan okunarak seriden çıkarılması](<../.gitbook/assets/image (43).png>)

Bu uygulama akışında sorun, programın **herhangi bir doğrulama yapmadan** verileri seriden çıkarmaya çalışmasıdır. Saldırgan serileştirilmiş verileri değiştirerek herhangi bir **saldırgan eylemi gerçekleştirmek** için uygulamaya gönderebilir.

## Örnek Saldırı Senaryoları

Bu bölümde PortSwigger Web Security Academy üzerinde yer alan “Lab: Modifying serialized objects” uygulaması üzerinden örnek bir saldırı senaryosu inceleyeceğiz. Bu uygulamada bizden yetkilerimizi yükseltmemiz ve Carlos kullanıcısına ait kullanıcıyı silmemiz isteniyor.

Öncelikle uygulamaya kendi kullanıcımız ile giriş yapalım.

![](<../.gitbook/assets/image (45).png>)

Uygulamaya başarılı bir şekilde giriş yapıldığında “session” isimli bir cookie atandığını görüyoruz.

| **Set-Cookie: session=Tzo0OiJVc2VyIjoyOntzOjg6InVzZXJuYW1lIjtzOjY6IndpZW5lciI7czo1OiJhZG1pbiI7YjowO30%3d; Secure; HttpOnly; SameSite=None** |
| ------------------------------------------------------------------------------------------------------------------------------------------- |

&#x20;Cookie verisi Base64 Encode ve URL encode edilmiş. Bu veriyi öncelikle URL Decode sonrasında da Base64 Decode ettiğimizde karşımıza aşağıdaki gibi bir veri çıkıyor.

| **O:4:"User":2:{s:8:"username";s:6:"wiener";s:5:"admin";b:0;}** |
| --------------------------------------------------------------- |

Bu veriyi anlamlandırmaya çalışalım. Veri içerisinde 4 karakteli “User” isimli nesnesi bulunuyor ve bu nesnenin 2 nitelik içerdiği belirtiliyor. İlk niteliğimiz 8 karakterli “username” niteliği ve bu niteliğe karşılık 6 karakterli “wiener” değeri atanmış. İkinci niteliğimizde ise 5 karakterli “admin” niteliği bulunuyor ve karşılığında da “boolean false” değeri atanmış.

Bu aşamada saldırgan olarak, “admin” niteliğinin yönetici haklarını temsil ettiğini ve bu niteliği “boolean true” olarak değiştirerek yönetim paneline erişim durumunu test etmeye çalışabiliriz. Cookie içerisindeki veri değiştirilerek aşağıdaki formatta hazırlanabilir.

| **O:4:"User":2:{s:8:"username";s:6:"wiener";s:5:"admin";b:1;}** |
| --------------------------------------------------------------- |

Gerekli encoding işlemlerini de yaptıktan sonra uygulama içerisinde oturumumuzu temsil eden session cookie değerini aşağıdaki hazırlamış olduğumuz “admin” session verisi ile değiştirebiliriz.

| **Tzo0OiJVc2VyIjoyOntzOjg6InVzZXJuYW1lIjtzOjY6IndpZW5lciI7czo1OiJhZG1pbiI7YjoxO30%3** |
| ------------------------------------------------------------------------------------- |

Session cookie’sini değiştirdiğimizde artık yönetim paneline erişim sağlayıp carlos kullanıcısını silebildiğimizi görüyoruz.

![](<../.gitbook/assets/image (26).png>)

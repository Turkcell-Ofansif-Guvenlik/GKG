# Güvenli Oturum Yönetimi için Dikkat Edilmesi Gerekenler

* Kullandığınız framework’ün sunduğu oturum denetimleri kullanılmalıdır.
* Oturum kimliği oluşturma, güvenilir bir sunucuda yapılmalıdır.
* Oturum tanımlayıcıları, yeterince rastgele üretilmelidir.
* Çerezlerin domain ve path öznitelikleri ayarlanmalıdır.
* Çıkış (Logout) işlemi yapıldığında, sunucu tarafında ilişkili oturum sonlandırılmalıdır.
* İş gereksinimine bağlı olarak, mümkün olduğunca kısa bir oturum hareketsizlik süresinin belirlenmesi önerilmektedir.
* Oturum etkinken bile kalıcı oturum açma işlemlerine izin verilmemeli, periyodik olarak oturum sonlandırma işlemi uygulanmalıdır.
* Oturumu açmadan önce bir oturum oluşturulduysa, başarılı bir şekilde giriş yapıldıktan sonra yeni bir oturum oluşturulmalıdır.
* Her başarılı kimlik doğrulama sonucunda, yeni bir oturum oluşturulmalıdır.
* Mümkünse, aynı kullanıcıya ait eş zamanlı oturum açılabilmesine izin verilmemelidir.
* Oturum tanımlayıcıları, URL’lerde, hata mesajlarında ve günlüklerde gösterilmemelidir.
* Herhangi bir ayrıcalık seviyesi değişikliğinden sonra oturum kimliğini yenilenmelidir. (Parola değişiklikleri, izin değişiklikleri gibi)
* Eğer, durum bilgisinin kullanıcı tarafında saklaması gerekiyorsa, şifreleme ve bütünlük denetimleri, sunucu tarafında kontrol edilmelidir.
* Cross-Site Request Forgery (CSRF) ataklarına karşı, güçlü ve rastgele bir token kullanarak koruma sağlanmalıdır.
* Çerezlerde “Secure” ve “HTTPOnly” öznitelikleri işaretlenmelidir.
  * Secure bayrağı, çerezin sadece güvenli bağlantılar üzerinden taşınmasını garanti altına alır. HTTPOnly bayrağı ise, javascript’in çereze erişmesini engeller. Böylelikle, olası bir XSS atağına karşı çerezin ele geçirilmesinin önüne geçer.

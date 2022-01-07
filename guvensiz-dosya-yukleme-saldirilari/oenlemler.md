# Önlemler

Yüklenecek dosyaların uzantıları her zaman kontrol edilmelidir. Özellikle birden fazla uzantı verilmiş dosyalara dikkat edilmelidir. Saldırganlar uzantı kontrolünü atlatmak için birden fazla dosya uzantısı ile dosya yüklemeye çalışabilirler.

Örneğin, .txt dosyası yüklenen bir uygulamada, sunucu tarafında yalnızca ilk uzantı kontrolü yapılıyorsa **filename.txt** isimli bir dosyada herhangi bir sorun çıkmayacaktır.

| <p><strong>String tokens[] = fileName.split(“\\.”);</strong></p><p><strong>String fileNameExtension = tokens[1];</strong></p> |
| ----------------------------------------------------------------------------------------------------------------------------- |

Ancak saldırgan JSP Shell dosyasına **filename.txt.jsp** adını verirse, kontrol yalnızca ilk uzantı olan .txt ile sağlanacak ve geçerli bir dosya uzantısı olarak kabul edilecektir. Ancak dosyanın gerçek uzantısı olan .jsp yükleneceği için saldırgan uzaktan komut çalıştırabilecektir. Yapılan kontrollerin **her zaman son dosya uzantısı** üzerinden sağlanması gerekmektedir.

| <p><strong>String extension = “”;</strong></p><p><strong>int i = fileName.lastIndexOf(‘.’);</strong></p><p><strong>if (i > 0)</strong></p><p>     <strong>extension = fileName.substring(i + 1);</strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Mümkünse yüklenen dosyalar üzerinde **virüs** **taraması** yapılmalıdır.

Yüklenen dosyalar ve uygulama kullanıcısı sistem üzerinde **minimum haklara** sahip olmalıdır.

Mümkünse dosya yüklemelerini yalnızca **kimlik** **doğrulaması** yapmış kullanıcılar yapmalıdır.

DoS (Denial of Service) ihtimalini düşürmek için dosya yükleme sayısına kısıtlamalar getirilmelidir. Dosya yükleme sınırı getirilmemiş uygulamalarda çok sayıda dosya yükleyen saldırganlar diski ve ağ trafiğini doldurarak uygulamanın çalışmasını engelleyebilir.

Yüklenecek olan dosyaya yeni isim verilmelidir. Kullanıcıdan gelen isimler doğrudan kabul edilmemelidir. Kullanıcıdan gelen dosya ismi **beyaz liste** kontrolden geçirilmelidir.

**Kara liste** girdi denetimi özellikle **tehlike** arz eder. Engellenecek tüm dosya uzantıları eklenemeyebilir / unutulabilir. Bunun yerine sadece izin verilen dosya uzantılarına izin verilmesi daha sağlıklı olacaktır.

Blacklist kontrollerde dosyaların farklı varyasyonları olduğu da unutulmamalıdır. Örneğin .php yerine .pHp, .php5, .phtml gibi uzantılar kullanılarak yazdığınız filtre atlatılabilir.

Karşıdan yüklenen dosya web veya uygulama dizini dışında bir yerde tutulmalıdır.

Yüklenecek dosyanın **boyutu** ve **içeriği** kontrol edilmelidir.

Dosya içeriği kontrol edilmeli, yalnızca içeriği, istenilen içerikte olan dosyalara izin verilmelidir. Resim dosyaları için **SecureImage** veya **ImageMagick** kütüphaneleri, daha kapsamlı içerik kontrolleri için **JHOVE** kullanılabilir. Ancak içerik kontrolü için 3.parti kütüphane kullanılacaksa **son versiyon** olmasına dikkat edilmeli, **zafiyetli bir sürüm kullanılmamalıdır.**

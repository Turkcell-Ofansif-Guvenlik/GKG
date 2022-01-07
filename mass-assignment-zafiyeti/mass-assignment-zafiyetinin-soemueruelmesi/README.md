# Mass Assignment Zafiyetinin Sömürülmesi

Bir önceki bölümden dikkatimizi çeken nokta UserModel sınıfımızdaki **“isAdmin”** ve **“isEnabled”** niteliklerinde karşımıza çıkıyor. Bu öznitelikleri istek üzerinde göndermediğimizde arka plandaki iş akışına göre varsayılan değerde tutulabilir veya boş bırakılabilir. Peki ya biraz kötü niyetli düşünüldüğünde nerelere varılabilir? Bu özniteliklerin üzerine yazma ihtimalimiz olabilir mi? Aynı isteği aşağıdaki şekilde tetikleyelim.

| <p><strong>POST /addUser</strong></p><p><strong>...</strong></p><p><strong>username=anilbas&#x26;password=C0kGizl!S1fr3&#x26;displayName=Anıl+Baş&#x26;emailAddress=test@testmail.com&#x26;organizationalUnit=test&#x26;organization=test&#x26;locality=Istanbul&#x26;stateProvince=Istanbul&#x26;countryCode=TR&#x26;isAdmin=true</strong></p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

| **Öznitelik**      | **Değer**         |
| ------------------ | ----------------- |
| username           | testuser          |
| password           | C0kGizl!S1fr3     |
| displayName        | Test User         |
| emailAddress       | test@testmail.com |
| organizationalUnit | test              |
| organization       | test              |
| locality           | Istanbul          |
| stateProvince      | Istanbul          |
| countryCode        | TR                |
| isAdmin            | **true**          |
| isEnabled          |                   |

Bu noktada artık **“isAdmin”** özniteliğini de ön yüzden eklenmemesine rağmen üzerine yazarak kendi kullanıcımızı backend sunucusunda yönetici yetkileri ile ekleyebildik. Yani uygulama üzerinde yönetici haklarını kendi hesabımıza da alabildik. Zafiyeti sömürebilmek için arka planda UserModel sınıfındaki nitelikleri bilmemiz gerekiyor. Farklı bir uygulamada bu nitelik isAdmin değil de doğrudan admin de olabilir. Bunu saldırganın bilebilmesi ise çok zor.

Saldırgan bu zafiyeti şu durumlarda sömürebilir;

* Arka planda sınıfa bağlı özniteliğin ismini tahmin edebilmeli veya,
* Kaynak koduna erişimi varsa (açık kaynak kodlu projeler için bu ihtimal yüksek ya da farklı bir zafiyeti sömürerek kaynak kodu görebiliyorsa mümkün olabilir) ve hassas alanlar için modelleri inceleyebilmeli,
* Ve bu alanları içeren sınıfın boş bir constructor yapısı olmalı.

#### **Örnek Olay**

2012 yılında, mass assignment zafiyeti kullanılarak GitHub’a saldırıda bulunuldu. Bir kullanıcının publickey bilgisini herhangi bir kuruluşa yüklemesi ve böylece kod kütüphanelerinde değişiklikler yapabilmesi bu saldırıya olanak sağladı. [GitHub'ın Blog Yazısı.](https://github.blog/2012-03-04-public-key-security-vulnerability-and-mitigation/)

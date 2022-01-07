# Önlemler

XSS saldırılarını engellemek için farklı durumlar için farklı çözümler uygulanmalıdır.

**Durum 1:**

Eğer doğrudan HTML yanıt üreten bir backende sahipseniz, HTML kodu backend üzerinde şablon işleme sonucunda elde edileceği için bu şablonları işleyen eden frameworkler doğru bir biçimde kullanılmalıdır.

Framework kullanımı her dilde ve her frameworkte farklılık göstermektedir. Genellikle string interpolation içerisinde yazılmış bir değişkenin içerisinde bulunan veriyi HTML kodlama ile işlerler.

Python dili Jinja şablon yöneticisinden örnek vermek gerekirse,

| <p><strong>{% for item in items %}</strong></p><p>        <strong>&#x3C;li>&#x3C;a href="{{ item.href }}">{{ item.caption }}&#x3C;/a>&#x3C;/li></strong></p><p><strong>{% endfor %}</strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

**item.href** ve **item.caption** değişkenlerinin içerisinde bulunan veri üretilen HTML çıktı üzerinde HTML kodlanmış formatta görülecektir.

**Durum 2:**

Eğer JSON formatında yanıt üreten bir backende sahipseniz, HTML kodunu ön yüz tarafında üretiyorsunuz demektir. Genellikle bu gibi durumlar için ReactJS, VueJS gibi teknolojiler kullanılmaktadır. Burada da birinci durumda olduğu gibi html kodunu üreten taraf önlemi almak durumundadır. Ön yüzde üretildiği için gelen değişken genellikle string interpolation içerisinde yazıldığı takdirde kullanılan framework otomatik olarak HTML Kodlama işlemini yapacaktır.

Her iki durumda da kilit nokta, eğer bir framework kullanılıyorsa doğru bir şekilde kullanılmalıdır. Eğer kullanılmıyorsa, veri hangi teknolojiye gönderilecek ise **o teknoloji için uygun kodlama** işlemi uygulanmalıdır.

Ayrıca oturum çerezleri belirlenirken **HTTPOnly** özniteliği ile işaretlenmesi oldukça önemlidir. Bu sayede aşağıdaki örnek saldırı senaryosunda da görülebileceği gibi, çerez verisine JavaScript ile erişim engellenecek, XSS ile bu değerin çalınması engellenmiş olacaktır.

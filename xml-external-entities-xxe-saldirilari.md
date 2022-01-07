# XML External Entities (XXE) Saldırıları

Güvenlik açıkları genellikle uygulamaların sunduğu özelliklerin kötüye kullanılmasından kaynaklanmaktadır. Bu sebeple, XML External Entity Injection (XXE) zafiyetinin ne olduğuna geçmeden önce XML yapısının sunduğu özellikleri incelememiz, zafiyetin neden kaynaklandığı anlayabilmemiz için fayda sağlayacaktır.

## XML

**XML (eXtensible Markup Language),** genel olarak veri depolamak ve farklı platformlar arasında veri taşımak üzere kullanılan işaretleme dilidir. Farklı teknolojiler ve ortamlar arasında verilerin ortak bir formatta taşınması amacıyla kullanılmaktadır. Yapı olarak HTML'e benzer ve istenildiği gibi özelleştirilebilir.

**Örnek XML Belgesi:**

| <p><strong>&#x3C;?xml version="1.0" encoding="UTF-8"?></strong></p><p><strong>&#x3C;person></strong></p><p>  <strong>&#x3C;name>Harold&#x3C;/name></strong></p><p>  <strong>&#x3C;surname>Finch&#x3C;/surname></strong></p><p>  <strong>&#x3C;description>XML Sample&#x3C;/description></strong></p><p><strong>&#x3C;/person></strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

Uygulamalar üzerinde, XML formatta gelen verilerin kullanılması için öncelikle **XML işleme** sürecinden geçirilmesi gerekir. Uygulama tarafında, gelen XML veriler üzerinde çeşitli işlemler yapmak isteyebiliriz. Örneğin, verileri alıp veri tabanına yazmak veya veriler üzerinde bazı işlemler uygulamayıp ekranda göstermek isteyebiliriz. Bu gibi durumlarda, ilk olarak XML verilerin ayrıştırılması (XML Parsing) gerekir.

XML Parsing işlemi için kullanılan programlama dilinin sunduğu standart kütüphaneler veya API'lar (XML Parser’lar) kullanılır. **XML Parsing** işleminin altını çizelim ve zafiyetin neden kaynaklandığını anlamak için XML'in sunduğu bazı özellikleri incelemekle devam edelim.

## Document Type Definition (DTD)

İlk özelliğimiz olan **Document Type Definition (DTD)**, XML belgesinin yapısını ve niteliklerini tanımlar. Bu durumu, veri tabanındaki alanları oluştururken kullandığımız yapıya benzetebiliriz. Örneğin, id alanı INT veya adres alanı VARCHAR 255 gibi tanımlamalara benzetebiliriz.

DTD'ler, XML belgesinin **içerisinde (internal)** tanımlanabileceği gibi **başka bir kaynak (external)** üzerinden de dahil edilebilir. Harici bir kaynağa erişim sağlamak için XML'in desteklendiği **SYSTEM** niteliğini kullanıyoruz. SYSTEM niteliği, **HTTP** ve **FILE** gibi protokolleri desteklemektedir.

Aşağıdaki örnekte, XML belgesinin olduğu dizindeki Person.dtd adlı dosyaya SYSTEM niteliği ile erişilerek, external DTD tanımlaması yapılmıştır.&#x20;

**External DTD tanımlanması:**

| <p><strong>&#x3C;?xml version="1.0" encoding="UTF-8"?></strong></p><p><strong>&#x3C;!DOCTYPE person SYSTEM "Person.dtd"></strong></p><p><strong>&#x3C;person></strong></p><p>  <strong>&#x3C;name>Harold&#x3C;/name></strong></p><p>  <strong>&#x3C;surname>Finch&#x3C;/surname></strong></p><p>  <strong>&#x3C;description>XML Sample&#x3C;/description></strong></p><p><strong>&#x3C;/person></strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

**Person.dtd dosyasının içeriği:**

| <p><strong>&#x3C;!DOCTYPE person</strong></p><p><strong>[</strong></p><p><strong>&#x3C;!ELEMENT person (name,surname,description)></strong></p><p><strong>&#x3C;!ELEMENT name (#PCDATA)></strong></p><p><strong>&#x3C;!ELEMENT surname (#PCDATA)></strong></p><p><strong>&#x3C;!ELEMENT description (#PCDATA)></strong></p><p><strong>]></strong></p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Aşağıdaki örnekte ise XML belgesi içerisinde (internal olarak) DTD tanımlaması yapılmıştır.

**Internal DTD tanımlanması:**

| <p><strong>&#x3C;?xml version="1.0" encoding="UTF-8"?></strong></p><p><strong>&#x3C;!DOCTYPE person [</strong></p><p><strong>&#x3C;!ELEMENT person (name,surname,description)></strong></p><p><strong>&#x3C;!ELEMENT name (#PCDATA)></strong></p><p><strong>&#x3C;!ELEMENT surname (#PCDATA)></strong></p><p><strong>&#x3C;!ELEMENT description (#PCDATA)></strong></p><p><strong>]></strong></p><p><strong>&#x3C;person></strong></p><p>  <strong>&#x3C;name>Harold&#x3C;/name></strong></p><p>  <strong>&#x3C;surname>Finch&#x3C;/surname></strong></p><p>  <strong>&#x3C;description>XML Sample&#x3C;/description></strong></p><p><strong>&#x3C;/person></strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

XML Parser, XML veriyi ayrıştırırken öncelikle DTD tanımını okur ve buradaki direktiflere göre XML'i yorumlar.

## Entities

İkinci özelliğimiz olan **Entity** kavramı ile devam edelim. Entity'ler XML'e dinamiklik katmak için tanımlanabilecek varlıklardır. Entity’leri, DOCTYPE ile birlikte kullanabiliyoruz ve hem **belge içerisinde (internal)** hem **** de **başka bir kaynak (external)** üzerinden tanımlayabiliyoruz.

Entity’lerin SYSTEM niteliğine erişimi vardır. Örneğin, başka bir kaynak üzerinden (dosya yolu veya URL) SYSTEM niteliği ile entity tanımlaması yapabiliyoruz. Tanımlandığımız bu entity’leri de XML belge içerisinde çağırabiliyoruz.

&#x20;

**Internal Entity Tanımlanması:**

| <p><strong>&#x3C;?xml version="1.0" encoding="UTF-8"?></strong></p><p><strong>&#x3C;!DOCTYPE person [</strong></p><p><strong>&#x3C;!ENTITY sample "Person Of Interest"></strong></p><p><strong>]></strong></p><p><strong>&#x3C;person></strong></p><p>  <strong>&#x3C;name>Harold&#x3C;/name></strong></p><p>  <strong>&#x3C;surname>Finch&#x3C;/surname></strong></p><p>  <strong>&#x3C;description>&#x26;sample;&#x3C;/description></strong></p><p><strong>&#x3C;/person></strong></p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

&#x20;****&#x20;

**External Entity Tanımlanması:**

| <p><strong>&#x3C;?xml version="1.0" encoding="UTF-8"?></strong></p><p><strong>&#x3C;!DOCTYPE person [</strong></p><p><strong>&#x3C;!ENTITY sample SYSTEM "https://example.com/test.dtd"></strong></p><p><strong>]></strong></p><p><strong>&#x3C;person></strong></p><p>  <strong>&#x3C;name>Harold&#x3C;/name></strong></p><p>  <strong>&#x3C;surname>Finch&#x3C;/surname></strong></p><p>  <strong>&#x3C;description>&#x26;sample;&#x3C;/description></strong></p><p><strong>&#x3C;/person></strong></p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

&#x20;

Buraya kadar anlatılan durumu özetleyelim. DOCTYPE üzerinden Entity tanımlamaları yapabiliyoruz. Entity’lerin SYSTEM niteliğine erişimi var ve SYSTEM niteliği üzerinden harici kaynaklara erişim sağlayabiliyoruz. Son olarak da XML belgemiz içerisinde tanımlanan entity’leri çağırarak, kullanabiliyoruz.

&#x20;

Zafiyetin anlaşılması için bazı XML özelliklerini ve temel yapıyı öğrendikten sonra artık zafiyet üzerine konuşmaya geçelim.

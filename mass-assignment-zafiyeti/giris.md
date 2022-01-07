# Giriş

Mass Assignment (toplu atama) zafiyeti, kök nedenine bakıldığı zaman çok basit bir mantık hatasının kötüye kullanımı ile ortaya çıkan bir zafiyettir. Temelinde yatan neden basit olsa da anlaşılması ve sömürmesi nispeten zor olabilmektedir.

Öncelikle zafiyet, isminden de anlaşılacağı üzere toplu olarak veri atanması ile oluşmaktadır. Zafiyeti anlayabilmek için öncelikle API ara yüzlerinde karşımıza çıkan bir ihtiyacı inceleyelim. Backend kodumuzda bir kullanıcı nesnesi olduğunu düşünelim ve bu kullanıcı nesnesinin modeli aşağıdaki gibi olsun.

![](<../.gitbook/assets/image (42).png>)

Kullanıcıdan alınan bilgileri alıp, kullanıcı modelini oluşturan “controller” yapımızda tüm bu parametreleri tek tek ayarlamak çok yönetilebilir bir süreç değil gibi, aynı zamanda modelin değişip daha fazla öznitelik eklenmesi gibi durumlarda geliştirme eforu çıkartabilir. Bunun yerine çoğunlukla API uç noktasına gelirken kullanıcıdan alınan tüm verilerin arka taraftaki UserModel sınıfına eşleştirilmesi çok daha kolay yönetilebilir görünüyor.

![](<../.gitbook/assets/image (1).png>)

Son durumda backend ortamımızda birçok öznitelik barındıran bir UserModel sınıfımız ve doğrudan API uç noktasına gelen veriyi UserModel sınıfı ile eşleştiren bir controller yapımız var. API uç noktasına aşağıdaki gibi bir form girdisinden alınıp işlenen verilerin gönderildiğini düşünelim.

Form girdisinden parse edilen API isteği aşağıdaki gibi oluşacaktır.

| <p><strong>POST /addUser</strong></p><p><strong>...</strong></p><p><strong>username=anilbas&#x26;password=C0kGizl!S1fr3&#x26;displayName=Anıl+Baş&#x26;emailAddress=test@testmail.com&#x26;organizationalUnit=test&#x26;organization=test&#x26;locality=Istanbul&#x26;stateProvince=Istanbul&#x26;countryCode=TR</strong></p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Bu normal istek controller tarafından karşılandığında UserModel sınıfımıza doğrudan bu parametreler eşleştirilecektir.

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
| isAdmin            |                   |
| isEnabled          |                   |


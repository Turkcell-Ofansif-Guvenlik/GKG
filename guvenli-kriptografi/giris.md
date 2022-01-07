# Giriş

Kriptografinin teorik ve pratik olarak farklı kullanımları bulunmaktadır. Bu kullanım alanları sayesinde birden fazla hedefin kontrol edilmesi ve güvenlik altına alınması sağlanabilmektedir.

**Gizlilik**; verinin yetkisiz kişiler tarafından okunamamasını sağlamasıdır.

**Veri Bütünlüğü**; verilerin değiştirilememesi, değiştirilmiş verinin tespit edilmesidir.

**Kimlik Doğrulama**; verinin bilinen aktörler tarafından geldiğinin kontrolüdür.

**İnkâr Edilemezlik**; verileri gönderen aktörün gönderdiğini inkâr edememesi.

Güvenli kriptografi konusunda en çok dikkat edilmesi gereken konulardan birisi **kodlamanın (encoding) şifreleme (encryption) olmamasıdır**. Bu iki kavram birbirleri ile çok karıştırılsa da birbirlerinden tamamen farklı kavramlardır. Kodlama (encoding) herhangi bir şifreleme sağlamaz ve geri dönüştürülebilir yapısından dolayı **açık metin (cleartext)** olarak kabul edilir.

Güvenlik kimlik doğrulama bölümünde de bahsettiğimiz gibi kritik veri içeren ayrıca kimlik doğrulama olan her sayfanın HTTPS kullanması gerekmektedir. Bu sayede hem sunucu ve kullanıcı arasında trafik şifreli bir şekilde iletilecek ve başka kişiler tarafından okunamayacak, hem de kullanıcı uygulamanın doğru uygulama olduğunu kontrol edebilecek, taklit bir uygulamada olmadığını doğrulayabilecektir.

Doğrudan kriptolama mekanizmalarına saldırmak oldukça zor ve sonuç alma olasılığı düşük olacaktır. Bu nedenle, saldırganlar ortadaki adam saldırıları (man-in-the-middle) ile sunucu üzerinden kullanıcı tarayıcısı üzerinden ya da iletim sırasında açık metin verileri almak için daha çok deneme yaparlar. Bu saldırılar başarı olasılıkları daha yüksek saldırılar olacaktır.

Son yıllarda bu saldırıların sayılarında artış görülmüş ve etkileri artmıştır. Saldırının başarılı olmasının temel nedeni hassas verilerin şifrelenmemesidir. Aynı şekilde zayıf şifreleme algoritmaları, cipher kullanımı da şifrelenmiş verinin elde edilebilmesine imkân sağlar.

Hassas veri ifşası zafiyetlerinde öncelikle uygulamada tutulan ve transfer edilen verilerin envanterinin olması gerekmektedir. Bu verilerin ele geçirilmesi halinde sorun olabilecekleri tespit edilmeli (kredi kartı, T.C. kimlik numarası, sağlık bilgileri, iş ya da kişisel bilgiler vb.), bu bilgilerin nasıl saklandıkları ve transfer edildikleri kontrol edilmelidir. Bu veriler HTTP, SMTP, FTP gibi güvenli olmayan kanallardan açık metin olarak gönderiliyor ise bu durum zafiyet oluşturacaktır.

Kritik verilen olduğu tüm sistemlerde TLS1.1 ya da daha üstü devreye alınmalı, tüm trafik şifreli olarak iletilmelidir. Bu zafiyetler ayrıca PCI gibi uyumlulukların alınmasına da engel olan zafiyetler arasında bulunmaktadır.

Şifreleme genel olarak simetrik ve asimetrik şifreleme olarak ikiye ayrılmaktadır. Güvenli kod geliştirme eğitimi kapsamında bu şifreleme algoritmalarının detaylarına girilmeyecektir. Yalnızca aradaki temel farklara değinilecektir.


# Güvenli Yazılım Prensipleri

Bir yazılımın güvenli olabilmesini sağlamak için dikkat edilmesi gereken genel prensipler bulunmaktadır. Bu prensiplere bağlı kalınması uygulamanın daha güvenli olmasını sağlayacağı gibi, sonrasında oluşabilecek olası vakalarda da daha hızlı aksiyon alınabilmesini sağlayacaktır.

Uygulamanın tasarımı **mümkün olduğunca basit** tutulmalıdır. Uygulama tasarımı karmaşıklaştıkça, saldırı yüzeyi arttığından dolayı risk daha çok artacaktır. Ayrıca **basit dizayn** edilmemiş uygulamalarda bir zafiyet tespit edilmesi halinde gerekli değişiklikleri yapmak daha zor olacaktır.

Uygulamalar çeşitli yetkilerle erişilebilen kaynaklar bulundurur. Uygulamada bulunan **her kaynağa erişim kontrolü** yapılmalı, yetkisiz kaynaklara erişimler verilmemelidir.

Tasarımlar içerisinde **sadece belirli kişilerin bildiği güvenlik önlemleri bulundurulmamalı**, alınan güvenlik önlemleri dokümante edilerek ilgili tüm ekipler tarafından bilinmelidir. Sadece belirli kişiler tarafından bilinen güvenlik önlemleri, kişilerin işten ayrılması vb. durumlarda bilinilirliğini yitirecek ve değişiklik, düzeltme yapmak çok zor olacaktır. Ayrıca güvenlik önleminin yeterli olup olmadığı **doğru test edilemeyecektir**.

Uygulama üzerinde gerekli loglar kayıt altına alınmalı, engellenemeyen durumlarda incelemelerin yapılması ve önlemlerin devreye alınması için kullanılabilir olmalıdır.

[Pareto ilkesine](https://tr.wikipedia.org/wiki/Pareto\_ilkesi) göre çoğu olayda **etkenlerin %20’si, etkilerin %80’ini gerçekleştirir**. Güvenli yazılımda bu ilkeyi sağlayan, en çok dikkat edilmesi gereken, en az eforla en çok zafiyetin engellenmesini sağlayan prensipler;

* Kullanıcıdan en az seviyede (yalnızca gerekli olanlar) girdi alınması,
* Kullanıcıdan alınan girdilerin kullanım amacına ve formatına yönelik uygun girdi denetiminden geçirilmesi ve
* Yetkilendirme

olarak sıralanabilir.

###

# Zafiyetli Bileşen Kullanımı

Uygulamalarda belirli amaçlar için var olan kütüphaneler, bileşenler ve yazılımlar kullanılabilir. Fakat kullanılan bileşen üzerinde halihazırda halka açıklanmış bilinen bir zafiyet olması bu bileşeni kullanan uygulamayı da tehlike altında bırakmaktadır. Bilinen zafiyetlerin sömürü kodlarının internet üzerinden aranması, bulunması ve bir kısmı için kullanması kolaydır. Uygulamaya özel olan zafiyetlerden farklı olarak bu zafiyetli sistemler için önceden yayınlanmış zararlı kodlar bulunabilir, tekrar yazılmasına gerek kalmayabilir.

Uygulamaların zafiyetlerinin olup olmadığının kontrolü kolay olsa da çok sayıda bileşen kullanan uygulamalarda bütün envanterin tutulmaması durumunda gözden kaçan bileşenler olmakta, bunların kontrollerinin yapılmaları atlanabilmektedir.

Tüm bileşenlerin güncellemelerinin ve zafiyetlerinin takiplerinin yapılabilmesi için öncelikle kullanılan bileşenlerin bir envanterinin oluşturulması gerekmektedir. Belirli aralıklarla ya da anlık takip ile bu bileşenlerin yeni versiyonları ve bilinen zafiyetleri takip edilebilir ve güncellemeler ile zafiyetlere karşı hızlı önlem alınabilir.

Amerikan kredi bürosu Equifax, Mayıs – Temmuz 2017 arasında veri sızıntısı açıklamıştı.  Bu ihlalde 147,9 milyon Amerikan vatandaşının özel kayıtları, 15,2 milyon İngiliz vatandaşı ve yaklaşık 19,000 Kanada vatandaşının güvenliği ihlal edilerek kimlik hırsızlığıyla ilgili en büyük siber suçlardan biri haline geldi.

Equifax'a yapılan veri ihlali, esas olarak yamalanmış, ancak Equifax'ın sunucularında güncellemediği üçüncü taraf bir yazılım açıklarından kaynaklanıyordu. Mart 2017 de çıkan Apache Strurs RCE zafiyetini sunucularında güncellemedikleri için çok büyük yaptırımlarla karşılaştılar. CVE-2017-5638 Struts2 uzaktan kod çalıştırma zafiyeti sunucular üzerinde uzaktan kod çalıştırılmasına ve sunucunun ele geçirilmesine neden olmaktadır. Bu bileşenin güncellenmemesi, sunucunun tamamen ele geçirilmesine ve buradan iç ağa yayılmasına neden olabilir.

Doğrudan uygulama üzerinde kullanılan bileşenler olmasa dahi, uygulamanın etkileneceği, kullanacağı bileşenlerin de güncellemeleri önemlidir. Bu güncellemelerin de hızlıca geçilebilmesi için gerekli çalışmalar yapılmalıdır.

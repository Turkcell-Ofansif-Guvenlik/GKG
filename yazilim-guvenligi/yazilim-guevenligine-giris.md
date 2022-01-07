# Yazılım Güvenliğine Giriş

Yazılım güvenliği, yazılımın **saldırı altında doğru bir şekilde çalışmaya devam etmesine** verilen isimdir. Yazılım güvenliğini temel olarak 3 ana kısımda inceleyebiliriz.

1. **Bütünlük:** Yazılımın işleyişinin ve servis ettiği verilerin bozulmaması.
2. **Gizlilik:** Yazılımın işlediği, servis ettiği gizli verilerin gizli kalması.
3. **Kullanılabilirlik:** Yazılımın servis vermeye devam edebilmesi.

## Hacker’lar ve Bakış Açısı

**Web ve mobil uygulamalar,** günümüzde sıkça kullanılan son derece kritik uygulamalardır. Güvenmediğimiz kullanıcılar ile kullanıcıların / çalışanların / şirketin verileri ile bir arayüz sağlar.

**Hacker'lar,** kullanıcılar için açılmış olan uygulamadaki **tasarım ve güvenlik hatalarından** yararlanarak, uygulamanın tasarım amacı dışında çalışmasını sağlayarak, firmaya, uygulamaya ya da diğer kullanıcılara **çeşitli zararlar** vermeyi amaçlayan saldırganlardır.

Uygulamadan fayda sağlamak için gelen "**gerçek kullanıcılar**" ile uygulamayı tasarımı dışında çalıştırmak için gelen "**saldırgan kullanıcılar**" aynı trafik protokollerini kullanır. Uygulamalar, kullanıcılar için oluşturulduğu için saldırganlar tarafından uygulamaların test edilememesini sağlamanın tam olarak olasılığı yoktur.

Geliştiriciler (developer) “**uygulama nasıl çalışmalı**” ve “**uygulama gereksinimleri nelerdir**” bakış açısı ile uygulamayı düşünürken. Saldırganlar “**uygulama ne için çalışır**” ve “**süreçler nasıl atlatılır**” bakış açısı ile uygulamayı incelemektedir.

Geliştirici ve saldırganların ortak noktaları her iki grubunda derinlemesine standart ve teknoloji bilgisi vardır ancak geliştirici işlerini kısıtlı zamanda yaparken, **saldırganların genellikle zaman sınırı yoktur**.

Bu durumda geliştiriciler uygulamalarını güvenli tasarlamak ve geliştirmek için saldırganların kullanabileceği temel güvenlik zafiyetlerini ve önlem mekanizmalarını bilmelidir. Çözüm sistemin **güvenli olarak tasarlanması ve geliştirilmesidir**.

## Yazılım Hatalarının Maliyeti

Güvenlik zafiyetlerine neden olmasalar dahi yazılımlarda bulunan **hataların (bug)** sonradan giderilmesi yöntemi oldukça **maliyetlidir**.

![https://medium.com/@raygunio/how-much-could-software-errors-be-costing-your-company-b44f19b3411e adresinden alınmıştır.](<../.gitbook/assets/image (28).png>)

Yukarıdaki şekilde de görüldüğü gibi yazılım **geliştirme aşamaları ilerledikçe fark edilen bugların maliyetleri daha da yükselmektedir**. Bunun nedeni, tasarım değişmesi, mimari değişmesi vb. konular olabileceği gibi, harcanan geliştirme eforundan dolayı **artan yazılımcı maliyeti** de olacaktır.

Bu hataların içlerinde **güvenlik açıklarına** neden olabilecek bugların bulunması ise bu **maliyetleri çok daha fazla artırır**. Güvenlik açıklarından kaynaklı saldırganların verdikleri hasarlar doğrudan maddi işlemler olabileceği gibi, uygulamanın itibarının düşmesi de olabilir. Uygulamanın itibarının düşmesi müşteri sayısını doğrudan etkileyeceği için bu gibi zafiyetlerin de sistemde bulunmaması uygulamanın kullanılabilirliği açısından oldukça önemlidir. Microsoft’un kurucusu Bill Gates’in 2002 yılında dediği gibi;

_“... great features won’t matter unless customers trust your software. So now, when we face a choice between adding features and resolving security issues, we need to choose security.”_

Bu nedenle oluşabilecek zafiyetlerin en aza indirilebilmesi için **yazılım geliştirme evrelerinin tamamında güvenlik göz önünde bulundurulmalıdır**.\


![](<../.gitbook/assets/image (41).png>)

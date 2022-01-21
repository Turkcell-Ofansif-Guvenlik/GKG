# Güvenli Kod Geliştirme Kitapçığı

Bu doküman Turkcell Ofansif Güvenlik - Uygulama Güvenliği takımı tarafından yazılmış olup, geliştirilmeye devam etmektedir.&#x20;

| Proje Lideri                   | Baş Yazar                                                                                                                                              | Katkıda Bulunanlar ve İnceleyenler                                         |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------- |
| <p>Anıl Baş<br>Haktan Emik</p> | <p>Anıl Baş</p><p>Emre Uzun</p><p>Emrecan Gerede</p><p>Haktan Emik</p><p>Mert Uğur</p><p>Muhammet Raşit Aydın</p><p>Onur Osman Güle<br>Semih Laçin</p> | <p>Ahmet Çağatay Beyaztaş<br>Esra Ercan<br>Fatih Demirbaş<br>Talha Şen</p> |

## Dokümanın Amacı

Uygulamalarının güvenliğinin sağlanması, firma ve kullanıcı verilerinin güvenliği açısından kritik önemdedir. Güvenli tasarlanmamış bir uygulama, diğer **kullanıcıların verilerine erişilebilmesine, bu kullanıcılar adına işlem yapılabilmesine** neden olabileceği gibi, uygulamanın bulunduğu **sunucunun da ele geçirilmesine**, buradan diğer sunuculara erişerek **kurum içerisinde saldırganın yayılmasına** neden olabilir.

Saldırganlar tarafından başarıyla gerçekleştirilebilen bu saldırılar, **maddi zarar ve itibar kaybına** neden olabileceği gibi, **KVKK** gibi bağlayıcı yasalar ve regülasyonlardan dolayı kurumun **ciddi cezalar almasına** neden olabilir.

Sunucuların güvenliğini sağlamak için yapılan çalışmalarda üzerlerinde bulunan web uygulamalarının da güvenli olması kritiktir. **Bir zincir en zayıf halkası kadar güçlüdür**.

**Güvenli Kod Geliştirme Dokümanı** uygulama geliştirilirken dikkat edilmesi gereken güvenlik zafiyetleri, sonuçları, etkileri ve zafiyetlerin çözüm önerilerini içermektedir.

Uygulama geliştirilirken birçok dil kullanıldığı ve bir doküman içerisinde her dil için örneklerin verilmesi mümkün olmadığından dolayı genel **bakış açısı ve dillere özel durumlar** aktarılacaktır.


# Server-Side Request Forgery (SSRF)

Sunucu Taraflı İstek Sahteciliği, bir saldırganın web uygulamasının sunucu tarafında saldırganın normalde dışarıdan erişemediği sistemlerle yetkisiz iletişim kurmasına olanak veren bir web uygulama güvenlik zafiyetidir. Bu hedefler sunucunun kendisi, iç ağdaki başka sistemler veya üçüncü parti sistemler olabilir. Erişilen sisteme bağlı olarak **veri ifşası**, **yetkisiz erişim** veya **yetkisiz erişime bağlı olarak diğer zafiyetlere** yol açabilir.

Aşağıdaki görseldeki gibi saldırgan web uygulaması üzerinden iç ağdaki sistemlere, uygulamanın kendisine veya üçüncü parti sistemlere erişim sağlamaktadır.

![https://portswigger.net/web-security/ssrf adresinden alınmıştır.](<../.gitbook/assets/image (30).png>)

Örnek olarak, kullanıcının belirli bir mağazada bir ürünün stokta olup olmadığını görmesini sağlayan bir alışveriş uygulamasını düşünün. Stok bilgilerini sağlamak için uygulamanın, söz konusu ürüne ve mağazaya bağlı olarak çeşitli backend REST API'lerini sorgulaması gerekir. Bu fonksiyon, bir HTTP isteği aracılığıyla ilgili backend API noktasına ileterek uygulanır. Bu nedenle, bir kullanıcı bir öğenin stok durumunu görüntülediğinde, tarayıcısı şöyle bir istekte bulunur:

| <p><strong>POST /product/stock HTTP/1.0</strong></p><p><strong>Content-Type: application/x-www-form-urlencoded</strong></p><p><strong>Content-Length: 118</strong></p><p> <strong></strong> </p><p><mark style="color:red;"><strong>stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1</strong></mark></p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Bu, sunucunun belirtilen URL'e istekte bulunmasına, stok durumunu almasına ve bunu kullanıcıya geri göndermesine neden olur.

Bu durumda, saldırgan, sunucunun kendisinde yerel bir URL belirtmek için isteği değiştirebilir.

**Örneğin:**

| <p><strong>POST /product/stock HTTP/1.0</strong></p><p><strong>Content-Type: application/x-www-form-urlencoded</strong></p><p><strong>Content-Length: 118</strong></p><p> <strong></strong> </p><p><strong>stockApi=http://localhost/admin</strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Burada sunucu /admin URL'sinin içeriğini alacak ve kullanıcıya geri gönderecektir. Bu durumda, saldırgan eğer iç ağdaki yönetim paneline erişemiyorsa bu erişimi localhost yani sunucunun kendisi üzerinden sağlayacak, eğer yönetim paneline erişim varsa ancak giriş yapamıyorsa localhost üzerinden erişim kontrolleri atlanarak, buraya tam erişim sağlayacaktır.

**Önlemler**

Örnekte görüldüğü gibi sorun kullanıcı tarafından gelen veriye tamamen güvenilmesinden ve erişim kontrollerinin eksikliğinden kaynaklanmaktadır. Zafiyetin giderilmesi için kullanıcı tarafından gelen verinin denetlenmesi, yukarıdaki örnekte URL’in alan adı kısmının kullanıcı kontrolünde olmaması gerekir. Veri denetiminde beyaz liste girdi denetimi uygulanması gerekir.

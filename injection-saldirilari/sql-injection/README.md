# SQL Injection

Kullanıcıdan gelen verinin tam ya da kısmi olarak SQL sorgusunda doğrudan kullanılması sonucunda SQL Injection zafiyeti oluşur. Başarılı bir SQL injection saldırısı veri tabanının tamamen ele geçirilmesine, hassas verilerin okunmasına, hatta sunucunun ele geçirilmesine, komut çalıştırılmasına neden olabilir.

Örneğin aşağıdaki kodun olduğu bir uygulama olduğunu düşünelim.

| **String query = "SELECT \* FROM accounts WHERE custID='" + request.getParameter("id") + "'";** |
| ----------------------------------------------------------------------------------------------- |

Burada kullanıcıdan gelen “id” parametresine hiçbir kontrol yapılmadan güvenilmekte ve bu parametre içerisindeki veri doğrudan SQL sorgusuna dahil edilmektedir. Ancak saldırgan aşağıdaki gibi bir istekte bulunduğu zaman SQL Injection zafiyetini sömürerek ilgili veri tabanından tüm hesap bilgilerini ele geçirebilir.

| **http://example.com/app/accountView?id=' or '1'='1** |
| ----------------------------------------------------- |

Aynı şekilde framework’lerin varsayılan koruma mekanizmalarına gözü kapalı güvenmek de aynı sonuca neden olacaktır. Aşağıdaki kod bloğunda HQL’e güvenildiğinden ham bir SQL sorgusu oluşturulmuş, oluşturulan sorgu özelinde kullanıcıdan alınan parametreye karşı önlem alınmamış ve bu güven SQL injection zafiyetinin devam etmesine neden olmuştur. Bu gibi ORM frameworklerinde ham SQL sorgusu oluşturmak yerine frameworkün sağladığı fonksiyonları kullanmakta fayda bulunmaktadır.

| **Query HQLQuery = session.createQuery("FROM accounts WHERE custID='" + request.getParameter("id") + "'");** |
| ------------------------------------------------------------------------------------------------------------ |

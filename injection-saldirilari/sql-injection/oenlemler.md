# Önlemler

## Prepared Statement

Prepared statement yapılarının amacı, SQL sorgusuna dahil edilecek verinin SQL teknolojisine uygun formatta kodlanarak, belirlenen konumlara map edilmesidir. Örneğin saldırgan tarafından kullanıcı adı olarak **admin’ or ‘1’ = ‘1** gönderildiğinde, kullanıcı adını tam olarak admin’ or ‘1’ = ‘1 olarak arayacak, tırnak işaretlerini karakter gibi görecek, 1 = 1 eşitliğini ve or işlemini mantıksal olarak almayacaktır.

**Prepared Statement yapısı için örnek Java kodu:**

| <p><strong>// This should REALLY be validated too</strong></p><p><strong>String custname = request.getParameter("customerName");</strong></p><p><strong>// Perform input validation to detect attacks</strong></p><p><strong>String query = "SELECT account_balance FROM user_data WHERE user_name = ?";</strong> </p><p><strong>PreparedStatement pstmt = connection.prepareStatement(query);</strong></p><p><strong>pstmt.setString(1, custname);</strong></p><p><strong>ResultSet results = pstmt.executeQuery();</strong></p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Stored Procedure

Prepared statement ve Stored Procedure arasındaki temel fark, Stored Procedure yapılarında SQL sorgusu veri tabanında prosedür olarak tanımlanıp veri tabanında tutulur ve daha sonra uygulama tarafından çağırılmaktadır. Her iki çözüm de temelinde aynı yöntemi kullandığından eşit derecede etkilidir. İş tasarımı ve ihtiyacına göre her ikisinden birisinin etkin bir şekilde kullanımı SQL Injection zafiyetlerinin önüne geçmek için yeterli olacaktır.

**Stored Procedure yapısı için örnek Java kodu:**

| <p><strong>// This should REALLY be validated</strong></p><p><strong>String custname = request.getParameter("customerName");</strong></p><p><strong>try {</strong>    </p><p> <strong>CallableStatement cs = connection.prepareCall("{call sp_getAccountBalance(?)}");</strong></p><p> <strong>cs.setString(1, custname);</strong></p><p> <strong>ResultSet results = cs.executeQuery();</strong></p><p> <strong>// Result set handling...</strong></p><p><strong>} catch (SQLException se) {</strong></p><p> <strong>// Logging and error handling...</strong></p><p><strong>}</strong></p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Beyaz Liste Girdi Denetimi

Kullanıcıdan gelen verilerin gerçekten beklenen verilerden birisi olup olmadığı beyaz liste yöntemi ile doğrulanır ve bu doğrulama işleminden sonra işleme alınır. SQL Injection ataklarına karşı kötü bir yazılım tasarımıdır ve bu şekilde yazılmış olan uygulamaların ilk fırsatta tekrar yazılması önerilir. Örneğin ID gibi nümerik alanların denetimi için beyaz liste girdi denetimi çözüm olabilirken, adres gibi zengin metin içerebilecek alanlar için beyaz liste doğrulaması yapmak zor olacaktır. SQL Injection ataklarına karşı özel olarak geliştirilmiş prepared statement ve stored procedure yapılarının kullanımı bu zafiyetleri engellemek için daha iyi bir tercihtir. Burada önemli olan noktalardan birisi de kara liste girdi denetiminin kensinlikle kulanılması gerektiğidir. Kara liste girdi denetimi atlatılması kolay bir önlem olduğundan dolayı güvenlik önlemi olarak değerlendirilmez.

## Kaçış İşlemi

Kullanıcı girdilerinin doğrudan sorgu üzerinde kullanılmadan önce kaçış (escape) işleminden geçirilmesidir. Her durumda SQL Injection saldırılarını önleyeceği **garanti edilemez.** Bu teknik, önceki çözümlerden hiçbiri uygun olmadığında son çare olarak kullanılabilir. Escaping işlemi için OWASP ESAPI Java ve 3.parti OWASP ESAPI .NET kütüphaneleri kullanılabilir. SQL sorgularında kaçış işlemi uygulanabilecek bazı özel karakterler;

| **‘ \ " % \_ &** |
| :--------------: |

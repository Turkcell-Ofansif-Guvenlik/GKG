# Insecure Direct Object Reference (IDOR) Saldırıları

Kullanıcılardan gelen güvensiz verilerin, sunucu tarafındaki bilgiler ile eşleştirilmesinde gerekli ve yeterli yetkilendirme kontrolleri uygulanmalıdır. Bu kaynaklara erişimlerde yetki kontrolleri yapılmadığı durumda saldırganlar kendilerine ait olmayan kaynaklara erişim sağlayabilir.

![](<../.gitbook/assets/image (31).png>)

IDOR saldırılarının nedenini anlatacağımız örnek uygulamamızda aşağıdaki gibi kullanıcıdan gelen veriyi doğrulamadan SQL çağrısı yaptığını düşünelim.

| <p><strong>pstmt.setString(1, request.getParameter("acct"));</strong></p><p><strong>ResultSet results = pstmt.executeQuery( );</strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------- |

Burada kullanıcı tarafından gönderilen hesap numarasının, işlemi yapan kullanıcı olup olmadığı kontrol edilmeden doğrudan SQL sonucu alınıyor. Bunu kullanan saldırgan aşağıdaki gibi bir istek ile istediği herkesin hesap bilgilerine erişebilir.

| **http://example.com/app/accountInfo?acct=notmyacct** |
| ----------------------------------------------------- |

Yine örnek olarak aşağıdaki URL’lerin yalnızca yönetici yetkisi olan kullanıcı tarafından görülebilmesi gerektiğini düşünelim.

| <p><strong>http://example.com/app/getappInfo</strong></p><p><strong>http://example.com/app/admin_getappInfo</strong></p> |
| ------------------------------------------------------------------------------------------------------------------------ |

Bu sayfalara giriş yapmamış kullanıcı ya da yönetici yetkisi olmayan kullanıcı erişebilirse burada da IDOR zafiyetinin olduğu söylenebilir.

IDOR zafiyetlerinin temel nedenlerinden birisi kullanıcıdan gelen kaynakları temsil eden verilerin (hesap numarası, profil kimliği, fatura kimliği vb.) kontrol edilmeden kullanılmasıdır.

&#x20;

Örnek olarak kullanıcının aşağıdaki istek ile kendi hesap bilgilerini görebildiğini düşünelim.

| **https://guvensizbankacilik.com/guvensizuygulama/hesapgoster.jspx?**_**id=2**_ |
| ------------------------------------------------------------------------------- |

Nesne referansı olarak kullanılan ID parametresi eğer sunucu tarafında kontrol edilmiyor ise, bu değeri değiştiren saldırgan, farklı kişilerin hesap bilgilerine erişebilir.

| **ID** | **İsim** | **Miktar** | **Hesap** |
| ------ | -------- | ---------- | --------- |
| 1      | Ali      | 123        | 98765     |
| 2      | Veli     | 456        | 56789     |

IDOR zafiyetlerini engellemek için, kullanıcıdan alınan verilere kullanıcının gerçekten erişim yetkisi olup olmadığının kontrolü yapılmalıdır. Uygulama üzerinde işlem yapmaya çalışan kullanıcı kendi oturum bilgisinden tespit edilebilir. Kaynağa erişim sırasında oturumdaki yetkisi ile erişilmek istenen kaynak arasındaki yetki kontrollerinin yapılması gerekir.

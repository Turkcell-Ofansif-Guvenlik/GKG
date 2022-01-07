# IP Kısıtlama

Yalnızca belirli IP’ler arasında trafiklerin olmasına imkân sağlayarak kimlik doğrulama yapar. Sabit IP’ler arasında kullanılması gerektiğinden, uygulamalar arasındaki kimlik doğrulamalara ek bir katman olarak kullanılır.

![](<../.gitbook/assets/image (18).png>)

| **HttpServletRequest.getRemoteAddr()** |
| -------------------------------------- |

Yukarıda gösterildiği gibi iki uygulama birbiri ile iletişim kurarken isteği yapan sunucunun IP adresi alınarak, beyaz liste girdi kontrolü ile istenilen sunucu olup olmadığı kontrol edilebilir. Ancak bu durum **aynı network** içerisinde oldukları durumda, arada Proxy olmaması durumunda geçerli olacaktır.

İki uygulama arasında proxy olması durumunda ise Uygulama - 1, proxy’nin kendi tarafında bakan arayüzüne isteği gönderecek, proxy ise Uygulama - 2’ye bakan arayüze bu isteği iletecektir. Proxy’nin her iki arayüzünde de farklı IP’ler olduğu için Uygulama - 2 isteği yapan sunucuyu Proxy’nin kendisine bakan arayüzü olarak görecektir.

Örnek olarak yukarıdaki gibi bir yapıda Uygulama - 2 kendisine gelen isteğin IP’sini ilk örnekteki gibi doğrudan almaya çalışırsa, proxy sunucusunun kendi tarafına bakan IP’sini görecektir.

| <p><strong>getIP()</strong></p><p><strong>192.168.2.2</strong></p> |
| ------------------------------------------------------------------ |

Bu durumda Uygulama - 2 eğer yalnızca Proxy IP’sini beyaz liste ile kontrol ederse, bu Proxy üzerinden kendisine gelen tüm isteklere güvenmiş olacak, buradan gelen yetkisiz sunuculara da izin vermiş olacaktır.

Örnekteki gibi Proxy üzerinden gelen isteklerin hangi IP’lerden geçtiğini kontrol edebilmemiz için **x-forwarded-for** başlığı bulunmaktadır. İstekler proxyden geçtikçe bu başlığın sonuna önceki IP’ler eklenir ve bu sayede trafik takip edilebilir. Yukarıdaki örnekte x-forwarded-for başlığı aşağıdaki gibi olacaktır.

| <p><strong>getHeader[“x-forwarded-for”]</strong></p><p><strong>192.168.4.3, 192.168.1.2</strong></p> |
| ---------------------------------------------------------------------------------------------------- |

Bu nedenle başlıkta bulunan **tüm IP’ler** kontrol edilmelidir. Yapılan bir diğer genel hata ise sadece ilk IP’nin kontrol edilmesidir. Bu durumda saldırgan kendi iç networkünde uygulamanın güvendiği bir IP’yi kullanırsa, kaynağın tamamına bakılmadığından Uygulama - 2 gelen isteğin geçerli bir sunucudan geldiğini varsayarak zararlı trafiği kabul edecektir.

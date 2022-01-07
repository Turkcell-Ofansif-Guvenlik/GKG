# Potansiyel Riskli HTTP Metotlarının Kullanımı

HTTP metotlarından bazıları bir saldırganın sunucuda bulunan dosyaları değiştirmesine ve bazı senaryolarda kullanıcıların kimlik bilgilerini çalmasına izin verdiğinden, bir web uygulaması için potansiyel olarak risk teşkil eder. Devre dışı bırakılması önerilen HTTP metotları şunlardır:

**PUT:** Bu yöntem istemci tarafından sunucu tarafına yeni dosyalar yüklemeye izin verir.  Saldırgan bu metodu sunucuya kötü amaçlı dosyalar yüklemek (Örneğin: Kabuk üzerinde komut yürüten bir ASP dosyası) veya sunucuyu kendi kişisel dosya deposu olarak kullanmak amacıyla çalıştırabilir.

**DELETE:** Bu yöntem istemci tarafının sunucu tarafında dosya silebilmesine olanak verir. Saldırganlar bu metot ile bir web sitesini kolaylıkla manipüle edebilir. Ayrıca Bir DoS saldırısı başlatmanın doğrudan bir yolu olarak da kolaylıkla bunu kullanabilir.

**CONNECT:** Bu yöntem bir istemcinin web sunucusunu Proxy olarak kullanmasına yol açabilir.

**TRACE:** Bu metot ile istek sunucuya gönderilen bilgi ne olursa olsun istemciye geri döner ve esas olarak hata ayıklama amacıyla kullanılır. Zararsız gibi gözükse de [Siteler Arası İzleme](https://www.cgisecurity.com/whitehat-mirror/WH-WhitePaper\_XST\_ebook.pdf) olarak bilinen bir saldırıyı başlatmak için kullanılabilir.

# Open Redirection

Open redirection (açık yönlendirme), uygulamanın güvensiz bir şekilde kullanıcıyı yönlendirme durumlarında karşılaşılan bir zafiyettir. Saldırgan, uygulama tarafından güvensiz yönlendirme yapıldığını keşfettikten sonra kendi zararlı uygulamasını, kullanıcılara oltalama yöntemi yayarak amacı doğrultusunda işlemler yaptırabilir.

Örnek bir yönlendirme işlemi aşağıdaki gibidir:

| **GET /app/redirect.php?url=http://legal-website.com** |
| ------------------------------------------------------ |

Saldırgan bu yönlendirmeyi kullanarak kendi sitesini URL parametresinin değerine yazar. Kullanıcının farketmemesi için URL kodlama ve base64 kodlama gibi yöntemler de izleyebilir. Dolayısıyla kullanıcı zararlı bir adrese yönlendirildiğinin farkına varmayabilir.

![https://www.business2community.com/cybersecurity/web-based-application-security-part-1-open-redirection-vulnerability-02184231 adresinden alınmıştır.](<../.gitbook/assets/image (23).png>)

#### Önlemler

Uygulamanın çalışma biçimine göre farklı çözümler mevcuttur.

Aşağıdaki iki yol ile zafiyet engellenebilir:

* Yönlendirme işleminde kullanıcı girdisi gerekli değil ise, yönlendirme fonksiyonu uygulamadan kaldırılmalı ve yerine doğrudan linkler konulmalıdır.
* Eğer yönlendirme işlemlerinde kullanıcı girdisine ihtiyaç duyuluyorsa, sunucu tarafında yönlendirilecek adresler için bir liste tutulmalı ve yalnızca bu sayfalara yönlendirmeye izin verilmelidir.

Aşağıdaki yollar ile de riskler azaltılabilmektedir:

* Uygulama yönlendirmelerinde sadece relative URL yapısı kullanabilir, bu yol ile saldırgan, uygulama dışına yönlendirilmemiş olur.
* Relative URL yapısı kullanılırken, URL kontrol edilmeli, slash ile başladığı teyit edilmeli ve önüne alan adı eklenerek yönlendirme edilmelidir.
* Uygulama Absolute URL kullanabilir tüm yönlendirmeleri için, fakat öncesinde ilgili alanın uygulamanın kendisi olup olmadığı kontrol edilmelidir.

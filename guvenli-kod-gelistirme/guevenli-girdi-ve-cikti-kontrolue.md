# Güvenli Girdi ve Çıktı Kontrolü

Girdi kontrolü, uygulamaya gelen bütün verilerin kullanılmadan önce doğru bir şekilde denetlenmesidir. Saldırıların birçoğunun temelinde yetersiz girdi kontrolü bulunmaktadır ve bu kontrol eksikliği sunucunun kontrolünün saldırganın eline geçmesine kadar birçok zarara neden olabilir.

Girdi kontrolü genel olarak **Kara liste / Engel listesi** (Blacklist / Deny List) olarak bilinen girdi kontrolü ve **Beyaz liste /İzin Listesi** (Whitelist / Allow List) olarak bilinen girdi kontrolü olmak üzere iki farklı yöntem ile yapılır.

## Kara Liste Girdi Kontrolü

Kara liste girdi kontrolünde bilinen kötü karakter veya karakter dizileri reddedilir. Varsayılan olarak **tüm girdileri işleme** eğilimindedir, yalnızca **istenmeyen** bir veri ile karşılaşıldığında **reddeder.** Bu yönü ile **tehdit odaklı** bir yaklaşımdır. Blacklist kontrolü oldukça yaygın olarak kullanılmaktadır ancak **güvensiz bir yöntemdir** ve **kullanılmamalıdır**.

Bilinen potansiyel zararlı karakterlerden olan **\<script>** ya da **or 1=1--** geçen girdilerin reddedilmesi işlemi kara liste girdi kontrolüne örnek olarak verilebilir.

**Örnek bir kara liste girdi denetimi:**

| <p><strong>List&#x3C;Pattern> blklistPttrns = new ArrayList&#x3C;Pattern>();</strong></p><p> <strong></strong> </p><p><strong>Pattern p = Pattern.compile(“&#x3C;script>”);</strong></p><p><strong>blklistPttrns.add(p);</strong></p><p> <strong></strong> </p><p><strong>for (Pattern aPattern : blklistPttrns){</strong></p><p>     <strong>//tam matching yapmıyoruz</strong></p><p>     <strong>if (aPattern.matcher(taintedInput).find())</strong></p><p>          <strong>//throw exception</strong></p><p><strong>}</strong></p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Burada fark edileceği gibi \<script> kelimesini tam olarak aramaktadır. Herhangi bir encoding işlemi ile gönderilmiş verileri kara liste ile bulmak oldukça zordur. Bunu yapmak için gelen verinin öncelikle normalize edilmesi (**Canonicalization**) gereklidir.

Örnek olarak **/../../etc/passwd** olarak gönderilen girdinin kara liste öncesinde normalize edilerek **/etc/passwd**’ye çevrilmesi gereklidir. URL encoding ile gönderilen **%27%20%6f%72%20%31** verisinin normalize edilmiş hali **‘ or 1** olacaktır.

Örnekten de anlaşılacağı gibi girdi denetimi **kritik ve karmaşık** bir işlemdir. Hatalı girilen değerler ve eklenmemiş değerlerin uygulama tarafından kabul edilebilecek olması da güvenlik açısından sorun olduğundan dolayı kullanılmamalıdır.

## **Beyaz Liste Girdi Kontrolü**

Beyaz liste girdi kontrolünde uygulama yalnızca onay verilen karakter veya karakter dizilerini kabul eder. Varsayılan olarak tüm girdileri **reddetme** eğilimindedir, yalnızca **kabul edilen** bir veri ile karşılaşıldığında işler. **Güven odaklı** bir yaklaşımdır. **Güvenli** ve **tavsiye** **edilen** girdi denetimidir.

Örnek olarak kredi kartı bilgilerinin alındığı bir girdi alanında gelen verinin öncelikli olarak kredi kartı numarası olup olmadığı kontrol edilmesi beyaz liste girdi kontrolü yapılmasıdır. Aynı şekilde e-posta adresi girilen bir alanda da girilen verinin işleme alınmadan önce e-posta adresi olup olmadığının kontrol edilmesi beyaz liste girdi kontrolüne dahildir.

Beyaz liste girdi kontrolünde mümkün olan en sınırlayıcı şekilde kontrollerin yapılması gerekmektedir. Örnek olarak bir alanda gelmesi beklenilen değerler yalnızca 1 ya da 0 ise veri geldiğinde ilk yapılması gereken işlem bu iki değerden birisinin olup olmadığının kontrolünün yapılması, bu değerlerden birisi değil ise işleme devam edilmemesi gerekmektedir.

Beyaz liste girdi kontrolünde sık yapılan hatalardan birisi de kontrollerin javascript ile tarayıcı üzerinde yalnızca istemci taraflı yapılmasıdır. Tarayıcı üzerinde yapılan kontroller uygulamaya gelen hatalı trafiği azaltacak, kullanıcıya anında bilgi vereceği için hata alma süresini kısaltıp, kullanıcı deneyimini artıracaktır. Ancak bu işlem kullanıcı bilgisayarı üzerinde yapıldığından dolayı kullanıcı bu kontrolleri devre dışı bırakabilir ya da HTTP Proxy ile sunucuya gitmeden hemen önce verileri değiştirebilir. Bu nedenle Javascript ile yapılan beyaz liste uygulamaları yalnızca kullanıcı deneyimini artırmak için kullanılabilir, **kesinlikle bir güvenlik sağlamaz**. Güvenli girdi denetimi için istemci tarafında yapılan girdi denetimine ek olarak sunucu tarafında da girdi denetimi yapılmalıdır.

**Örnek bir beyaz liste girdi denetimi:**

| <p><strong>List&#x3C;Pattern> = whtlistPttrns = new ArrayList&#x3C;Pattern>();</strong></p><p><strong>aPattern = Pattern.compile(“[a-zA-Z0-9]{2,100}”);</strong></p><p><strong>whtlistPttrns.add(aPattern);</strong></p><p> <strong></strong> </p><p><strong>for (Pattern aPattern : whtlistPttrns){</strong></p><p>     <strong>//tam matching yapıyoruz</strong></p><p>     <strong>if (!aPattern.matcher(taintedInput).matches())</strong></p><p>          <strong>// throw exception</strong></p><p><strong>}</strong></p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

## **Kodlama (Encoding) İşlemi**

Kodlama işleminin genel tanımı, girdi içindeki özel karakterlerin kullanıldığı bağlam özelinde bir formata değiştirilmesidir. **Kodlama işlemindeki amaç hedef yorumlayıcı için özel karakterlerin kodlama işlemi sonrası önemlerini yitirmiş olmasıdır.** Farklı hedef yorumlayıcılar için farklı kodlama işlemlerinin yapılması, zararlı kodların çalışmaması konusunda fayda sağlamaktadır.

Özellikle sınırlı sayıda olasılığı olmayan girdi alanlarında beyaz liste uygulamanın imkânı bulunmayacaktır. Blacklist kontrolü ise tam bir güvenlik sağlamadığından, bu durumlarda kullanılması gereken güvenlik denetimi kodlama işlemlerinin yapılmasıdır. Bu işlemi yapan, kütüphaneler bulunmaktadır. Hedef yorumlayıcıya göre özelleşmiş bu teknolojilerin kullanılması güvenliği sağlayacaktır.

Kodlamaya örnek olarak [HTML](https://en.wikipedia.org/wiki/Character\_encodings\_in\_HTML) ve [URL](https://en.wikipedia.org/wiki/Percent-encoding) kodlama verilebilir.

Aşağıda [OWASP ESAPI](https://owasp.org/www-project-enterprise-security-api/) tarafından sağlanan bazı kodlama örneklerini bulabilirsiniz.

| **String encJS = ESAPI.encoder().encodeForJavaScript(input);** |
| -------------------------------------------------------------- |

| **String encURL = ESAPI.encoder().encodeForURL(input);** |
| -------------------------------------------------------- |

| <p><strong>Codec c = new MySQLCodec(MySQLCodec.Mode.STANDARD);</strong></p><p><strong>String escSQL = ESAPI.encoder().encodeForSQL(c, input);</strong></p> |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------- |

| <p><strong>Codec c = new OracleCodec();</strong></p><p><strong>String escSQL = ESAPI.encoder().encodeForSQL(c, input);</strong></p> |
| ----------------------------------------------------------------------------------------------------------------------------------- |

Örneklerde de görülebileceği gibi kodlama işleminde önemli olan, hedef yorumlayıcıya uygun kodlama biçimini seçmektir. Aksi takdirde doğru kodlama yapılamayacağı için istenmeyen verilerin kabul edilmesi ile karşılaşılabilir.

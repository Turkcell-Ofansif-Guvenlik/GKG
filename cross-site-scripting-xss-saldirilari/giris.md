# Giriş

XSS zafiyetleri oldukça sık karşılaşılan zafiyetlerdir. XSS zafiyetleri genel olarak kullanıcıdan gelen verinin, filtrelenmeden, doğrulanmadan, ilgili denetim ve temizlik işlemlerinden geçirilmeden ve çıktı kodlaması yapılmadan doğrudan çıktı içerisine yazılması ile oluşur. Tarayıcı tarafından yorumlanabilecek uygun bir script parçasının (HTML, JavaScript vb.) kontrol edilmeden ekrana basılması sonucunda, burada gönderilen kodun tarayıcı tarafından anlamlandırılması yoluyla belirtilen işlemi gerçekleştirmesi ile gerçekleşir.

Örnek olarak kullanıcının girdiği bir metni kontrol etmeden ekranda gösteren bir sayfamız olsun. Buradan kullanıcı \<script>alert(1)\</script> gönderdiğinde, bunu doğrudan ekrana basan uygulama, tarayıcının javascript alert vermesine neden olacaktır. XSS saldırılarının kanıtlanmasında kullanılan bu alert işlemi, bu saldırılar ile yapılabilecek en masum işlemdir. Kurbanın tarayıcısında birçok farklı işlemin gerçekleştirilmesi için XSS saldırıları kullanılabilir.

XSS ile yapılabilecek saldırılar arasında, kullanıcı oturumunu çalma, çok faktörlü doğrulamaları atlatma, kullanıcıya zararlı yazılım indirme, tuş dinleme ve hatta CSRF token atlatılması bulunmaktadır.

XSS saldırıları doğrudan sunucu ya da uygulamaya yönelik yapılan saldırılar değildir. Ancak uygulamadaki bir güvenlik eksikliğinden yararlanarak, uygulamanın kendisini kullanarak yapılan bir saldırı olduğundan dolayı, kullanıcılara zarar verirken, uygulama ve firma imajına ciddi zararlar verecektir.

XSS saldırıları 3 çeşit olarak karşımıza çıkmaktadır.

## Yansıtılan (Reflected) XSS

Kullanıcıdan gelen verinin doğrudan ekranda gösterilmesi ile oluşur. Genellikle GET metodu parametresi olarak URL üzerinde gönderilir. Zafiyetin tetiklenmesi için genellikle sosyal mühendislik saldırıları ile birlikte hedefli olarak kullanılır. Sunucuda bir yere gönderilen değerler kaydedilmez, sadece gönderme anında kullanıcının tarayıcısında çalışır.

## Depolanan (Stored) XSS

En tehlikeli XSS saldırısıdır. Saldırı tekniği açısından yansıtılan XSS ile aynıdır ancak bu kez saldırgan tarafından gönderilen zararlı script uygulama üzerinde kaydedilir. Zararlı içerik uygulama üzerinde kaydedildiği için her kullanıcı tarafından görüntülenir. Örneğin bir yorum paylaşma ara yüzünde yazılan zararlı kodun veri tabanına kaydedilmesi ve sonrasında her ziyarette yorum alanındaki zararlı kodun görüntülenmesi gibi senaryolarla karşımıza çıkabilir.

## DOM XSS

Yansıtılan XSS ile oldukça benzer yapıda olsa da saldırılan parametre JavaScript API’ları üzerinde kullanılan yapılardır. Saldırı metodu ve etkileri bakımından yansıtılan XSS ile bir farkı yoktur.

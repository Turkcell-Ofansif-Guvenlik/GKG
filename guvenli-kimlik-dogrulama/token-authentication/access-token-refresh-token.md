# Access Token – Refresh Token

Bu yetkilendirme yönteminde oturum açan kullanıcıya access token ve refresh token olmak üzere iki token verilir. Access token isminden de yola çıkarak kaynaklara erişim için kullanılan token türüdür. Refresh token ise elimizdeki token çiftini yenilemek için kullanılan bir token türüdür. Jenerik bir uygulama akış diyagramı aşağıdaki gibidir.

![https://docs.wso2.com/display/IS530/Refresh+Token+Grant adresinden alınmıştır.](<../../.gitbook/assets/image (22).png>)

Bu yapıda access tokenların yaşam süresi çok kısadır, refresh tokenlar ise nispeten biraz daha uzun süreli olabilir. Yapı, kullanıcıdan bir kez kullanıcı bilgilerini girmesini ister ve bundan sonraki süreçte oturum yenilemesi için dahi kullanıcıdan kimlik bilgileri alınmaz. Bu durum “sonsuz oturum” sağlayacağından dikkat edilmelidir. Saldırgan kullanıcı refresh token ile mevcut sürekli oturumu yenileyerek işlemlere devam edebilir. Bu gibi şüpheli durumlarda kullanıcının mevcut tüm tokenlarının sonlandırılıp edilip, yeniden giriş yapması zorlanabilir.

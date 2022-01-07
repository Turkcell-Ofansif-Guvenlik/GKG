# LDAP Injection

LDAP (Lightweight Directory Access Protocol), dizin servislerine erişmek için kullanılan TCP/IP tabanlı bir protokoldür. Kullanıcıdan alınan girdinin, herhangi bir kontrolden geçirilmeden LDAP sorgusuna dahil edildiği durumda ortaya çıkar. Saldırgan, LDAP tarafından farklı yorumlanan meta karakterleri, girdi olarak göndererek, sorguya müdahale edebilir. LDAP injection saldırıları, kimlik doğrulama mekanizmalarının atlatılabilmesine, yetkilerinin olmadıkları sorgu ve bilgilere erişilebilmesine, LDAP ağacında yetkisiz modifikasyonlar yapabilmesine olanak sağlar.

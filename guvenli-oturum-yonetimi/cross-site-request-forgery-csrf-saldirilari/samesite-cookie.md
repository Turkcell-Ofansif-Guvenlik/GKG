# SameSite Cookie

Tarayıcıların çerez ekleme davranışı güvenlik problemlerine yol açtığı için çerezler tarafında SameSite özniteliği geliştirildi. SameSite özniteliğini kullanarak tarayıcıların çerez ekleme davranışı kontrol edilebilir. Bu tanımlama ile farklı bir kaynaktan tetiklenen isteklere çerezin hangi durumlarda eklenebileceği talimatı verilebilir.

SameSite özniteliğinin 3 farklı tanımlaması bulunuyor:

1. Strict
2. Lax
3. None

**Strict** olarak tanımlanması durumunda, başka bir kaynak üzerinden yapılan hiçbir isteğe çerez bilgisi eklenmez. Strict, en katı SameSite tanımlamasıdır.

| **Set-Cookie: SessionId=xxxxx; SameSite=Strict** |
| ------------------------------------------------ |

**Lax** olarak tanımlanması durumunda, başka bir kaynak üzerinden yapılan bazı isteklerde çerez bilgisi isteğe eklenir. Strict’e göre daha esnek bir tanımlamadır. Başka bir kaynak üzerinden yapılan HTTP GET işlemleri ve Top-Level Navigation işlemlerde yani tarayıcı adres çubuğunda URL’in değiştiği durumlarda çerez bilgisi isteklere eklenir.

| **Set-Cookie: SessionId=xxxxx; SameSite=Lax** |
| --------------------------------------------- |

Örnek olarak, link tanımlamalarında Top-level değişikliğe sebep olacağı için Lax tanımlaması yapıldığında çerez eklenirken,

| **\<a href="…">** |
| ----------------- |

Bir resim kaynağını yüklerken GET talebi yapılmasına karşın top-level değişikliğe sebep olmadığı için Lax tanımlaması yapıldığında çerez eklenmez.

| **\<img src="…">** |
| ------------------ |

_Chrome 80 versiyonu ile eğer SameSite tanımlaması yapılmaz ise çerezler varsayılan olarak Lax olarak değerlendirilir._

**None** olarak tanımlanması durumunda, SameSite özniteliğini kullanmak istenilmediği belirtilir. Bu durum, tarayıcıların başka bir kaynak üzerinden yapılan isteklere çerez bilgisini ekleyeceği anlamına gelir.

| **Set-Cookie: SessionId=xxxxx; SameSite=None; Secure** |
| ------------------------------------------------------ |

_Eğer, None olarak kullanmak istiyorsanız tarayıcılar, Secure özniteliği ile kullanılmasını şart koşuyor._

Hangi tarayıcı sürümlerinde SameSite cookie'nin desteklendiğini incelemek için: https://caniuse.com/?search=SameSite

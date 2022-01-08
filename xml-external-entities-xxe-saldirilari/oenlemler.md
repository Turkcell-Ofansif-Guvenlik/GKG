# Önlemler

XXE zafiyetinin giderilmesi için XML Parser üzerinde, DOCTYPE ve Entity işlemcileri devre dışı bırakılmalıdır. Bazı XML Parser’lar üzerinde bu özellikler varsayılan olarak devre dışı bırakılmış olsa da kullanılan XML Parser’ın yapılandırmasında bu özelliklerin devre dışı bırakıldığından emin olunmalıdır.&#x20;

**Örnek olarak;**

![ SAXParserFactory sınıfında bu özellikleri devre dışı bırakmak](<../.gitbook/assets/image (4).png>)

Daha fazla bilgi edinmek için OWASP tarafından hazırlanan [XXE Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/XML\_External\_Entity\_Prevention\_Cheat\_Sheet.html) incelenebilir.

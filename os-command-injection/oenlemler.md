# Önlemler

Eğer uygulamanın sistem prosesleri ile bir etkileşim sağlaması gerekmiyorsa sistem proseslerini çalıştıracak komut blokları kullanılmamalıdır. Eğer bu gibi bir ihtiyaç varsa OS komutlarını doğrudan çağırmak yerine ilgili yazılım dilinde yer alan built-in fonksiyonları kullanmayı tercih edebilirsiniz.  Örneğin system("mkdir /dir\_name") yerine Java.io.File.mkdir() gibi metodların kullanımı söz konusu olabilir.

Uygulamayı çalıştıran kullanıların mümkün olduğunca minimum OS komutu çalıştıracak şekilde yetkilendirilmesi önerilir. Bu durumda olası bir komut çalıştırma eyleminde işletim sistemi tarafından işlemler kısıtlanır.

OS command injection saldırılarının engellenmesi için en önemli yöntemlerden birisi de girdi denetimi yapılmasıdır. Ancak burada girdi denetimi yapılmadan önce, girdinin parametrelere ayrılması gerekmektedir. Komut ve argümanlar birbirinden ayrılmalı ve sunucuya bu şekilde gönderilmelidir.  Daha sonra gelen verilerin doğrulaması yapılmalıdır. Komut ve argümanlar farklı parçalar halinde geldiğinden farklı girdi denetim kuralları uygulayabilmek mümkün olacaktır.

Komutlar için; beyaz liste girdi denetimi yaklaşımı kullanılabilir. Bu sayede yalnızca sınırlı sayıda, önceden belirlenmiş ve yetkilendirilmiş komutlarım kullanımına izin verilebilir.

Argümanlar için ise sınırlı sayıda argüman seçeneği varsa beyaz liste yöntemi uygulanabilir. Gelebilecek argümanlar listesi çok kısıtlı ya da belirli değilse beyaz liste düzenli ifadeler kullanılabilir. Bu durumda kullanıcı tarafından gelebilecek sakıncalı olmayan karakterler ve bir uzunluk sınırı belirtilmelidir. Aşağıdaki karakterlerin izin verilen karakterler listesinde olmamasına dikkat edilmelidir.

| **& \| ; $ > < \ \ !\`** |
| :----------------------: |

Örnek olarak yalnızca rakam ve harflerin gelebileceği, 3 ve 10 arasında karakterin kabul edileceği bir argüman alanı için aşağıdaki gibi bir beyaz liste düzenli ifadesi kullanılabilir.

| **^\[a-z0-9]{3,10}$** |
| :-------------------: |

Aşağıda OS command injection zafiyetine neden olacak zafiyetli yazılmış Java kodunu bulabilirsiniz.

| **ProcessBuilder b = new ProcessBuilder("C:\DoStuff.exe -arg1 -arg2");** |
| :----------------------------------------------------------------------: |

Komut ve argümanların ayrı gönderildikleri ve bu sayede kontrollerinin yapılabileceği Java kodu ise aşağıda bulunmaktadır.

| <p><strong>ProcessBuilder pb = new ProcessBuilder("TrustedCmd", "TrustedArg1", "TrustedArg2");</strong></p><p><strong>Map&#x3C;String, String> env = pb.environment();</strong></p><p><strong>pb.directory(new File("TrustedDir"));</strong></p><p><strong>Process p = pb.start();</strong></p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

# OS Command Injection

OS command injection saldırıları web arayüzü aracılığıyla OS komutlarının çalıştırılması durumunda oluşan zafiyetlerdir. Kullanıcı girdilerinin kontrolsüz olarak OS komutlarına dahil edilmesi sonucu oluşur. Örnek olarak aşağıdaki gibi url sonuna saldırı denemesi yapılmış olsun.

| **http://sensitive/something.php?dir=%3Bcat%20/etc/passwd** |
| :---------------------------------------------------------: |

Örnek URL üzerindeki %3B karakteri URL kodlanmış bir veridir, düz metin karşılığı ise noktalı virgül işareti anlamına gelir ve terminal ortamındaki OS üzerinde komutlarını ayırmakta kullanılır. Bu işlem sonucunda /etc/passwd dosyası ekrana yazılıyorsa OS injection zafiyeti bulunuyor demektir.

Örneğin ağ üzerinde aktif cihazları kontrol edebilmek için aşağıdaki gibi cihazlara ping atan bir kod parçamız olsun.

| **ProcessBuilder b = new ProcessBuilder("ping " + ip);** |
| :------------------------------------------------------: |

IP değeri kullanıcıdan alınan bir değer ve herhangi bir doğrulamadan geçirilmediği takdirde saldırganlar aşağıdaki gibi bir saldırı ile bu kod parçasından OS Command Injection zafiyeti tetikleyebilir.

| **https://vulnerable.com/checkStatus?ip=192.168.1.1%3Bwhoami** |
| :------------------------------------------------------------: |

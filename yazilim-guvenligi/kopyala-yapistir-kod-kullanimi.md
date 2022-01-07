# Kopyala – Yapıştır Kod Kullanımı

Yazılım geliştirirken belirli işlevleri olan fonksiyonlar, zamandan tasarruf sağlamak ve proje teslim tarihlerini yakalamak için hazır kod bloklarından yararlanılarak geliştirilebilmektedir. Bu noktada elbette tekerleği yeniden keşfetmeye ihtiyaç yok, gereksinim duyulduğunda hazır kütüphaneler ve kod blokları kullanılması uygun görülebilir fakat kullanılan kod bloklarının güvenlik zafiyeti içermesinin de ihtimal dahilinde olduğu unutulmamalıdır. Hazır kod bloklarından alıntı yaparken, bu kod blokları içerisinde var olan güvenlik zafiyetlerinin de alıntılanması ihtimal dahilindedir. Ayrıca, kullanılacak kodun projeye dahil edilmesi esnasında yanlış yapılandırılması durumunda da güvenlik problemleri ile karşılaşılabilir.

Bu konuya dikkat çekmek için yapılan bir çalışmada geliştiriciler arasında çok popüler olan “stackoverflow” sayfasında yer alan C++ kod blokları incelenmiş ve aşağıdaki çıktılara ulaşılmıştır:

* 2560 tekil kod bloğu incelemeye alınmış ve bu kod bloklarından 69’unun güvenlik zafiyeti içerdiği tespit edilmiştir.
* 69 kod parçası içerisinde 29 farklı güvenlik zafiyetine referans verilmiştir.
* 2560 kod bloğu içerisinde zafiyetli 69 kod bloğunun bulunması çok görünmeyebilir fakat bu kod blokları GitHub üzerinde tarandığında 2800’ün üzerinde gerçek **canlı ortam kodlarının** bu zafiyetli kod bloklarını içerdiği tespit edilmiştir.

İlgili çalışma için https://stackoverflow.blog/2019/11/26/copying-code-from-stack-overflow-you-might-be-spreading-security-vulnerabilities/ adresini ziyaret edebilirsiniz.

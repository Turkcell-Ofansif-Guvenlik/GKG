# Önlemler

Deserialization saldırılarını önlemek için genel kurallar aşağıdaki gibidir.

1. **Dilden bağımsız formatlar kullanımı:** “Native Binary” formatlar yerine standart JSON, YAML gibi formatlar kullanılmalıdır.
2. **Bütünlük kontrolleri:** Eğer mümkünse, serileştirilmiş veriler için dijital imza doğrulaması yapılmalıdır. Bu kontrollerle birlikte kullanıcı tarafından sağlanan zararlı girdilerden kaçınılabilir.
3. **Girdi denetimleri:** Kullanıcı tarafından sağlanan verilere asla güvenilmemelidir ve mümkünse serileştirme işlemlerinde kullanıcı girdilerine yer verilmemelidir.
4. **Düşük yetkili ortam:** Seriden çıkarma işlemleri en az yetki barındıran ortamlarda, en az yetki çalıştırabilen kullanıcılar ile yapılmalıdır.

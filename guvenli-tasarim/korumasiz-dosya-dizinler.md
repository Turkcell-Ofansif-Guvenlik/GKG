# Korumasız Dosya / Dizinler

Client tarafından ulaşılan herhangi bir dosya veya dizinin doğrudan zafiyete yol açması söz konusu değildir. Ancak ulaşılan dosya içeriklerinin veya dizin isimlerinin hassas bilgilere sahip olması durumunda tehlikeye girilmektedir. Bu duruma örnek olarak sistem veya database versiyon bilgisi içeren bir dosyaya erişim verilebilir.&#x20;

Ayrıca bir örnek daha verilmesi gerekirse: upload sisteminde zafiyet içeren bir sosyal medya sitesinde profil fotoğraflarının olduğu dizine erişimin açık olduğunu düşünelim. Bu durum zaten kendi başına istenmez. Sebebi profil fotoğrafı gizli olan kullanıcılarında fotoğraflarına bu dizinden erişilebilmesidir. Birde sistemde file upload zafiyeti barınıyorsa. Saldırgan sunucu tarafına backdoor içeren, profil resmi süsü verdiği bir dosya yükleyip bu dizin üzerinden çalıştırabilme imkânı bulmaktadır.

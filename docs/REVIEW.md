# Mini-CRM Projesi – Kod İnceleme Raporu

**Kod İncelemeyi Yapan:**  
MOHAMMED ABDULRAHMAN ABDO ABDULLAH AL-HAMIDI  

**Öğrenci No:** 245112073  

---

## 1️ Projenin Genel Görünümü

- Node.js ve Express tabanlı bir REST API’dir  
- Müşteri, sipariş ve ürün yönetimi sağlamaktadır  
- ORM olarak Sequelize kullanılmıştır (model ve migration yönetimi)  
- Excel dosyalarından veri aktarımı için xlsx kütüphanesi kullanılmıştır  
- Swagger UI (/api-docs) ile API dokümantasyonu mevcuttur  
- Winston ve Trace-ID ile loglama ve izlenebilirlik sağlanmıştır  
- Geliştirme ortamında SQLite, üretim ortamında PostgreSQL uyumluluğu hedeflenmiştir  

---

## 2️ Güçlü Noktaları

- Katmanlı mimari uygulanmıştır (routes → services → models)  
- Telefon normalizasyonu ve mükerrer kayıt kontrolü yapılmaktadır  
- Müşteri kaydı olmadan misafir sipariş oluşturulabilmektedir  
- Swagger UI ve `docs/` klasörü altında gerekli dokümantasyon mevcuttur  
- Jest ve Supertest kullanılarak temel endpoint testleri yazılmıştır  
- Mock/Stub kullanımı ile servis katmanı izole şekilde test edilmiştir  
- Transaction desteği ile stok kontrollü sipariş oluşturma sağlanmıştır  
- Soft-delete mekanizması ile müşteri geçmişi korunmaktadır
- Migration dosyaları ile veritabanı şeması versiyonlanmıştır  

---

## 3️ Geliştirilmesi Gereken / Eksik Yönler

- Test kapsamı sınırlıdır, tüm servisler test edilmemiştir  
- CI/CD pipeline (GitHub Actions vb.) bulunmamaktadır  
- Input validation ve bazı güvenlik önlemleri eksiktir  

---

## 4️ Öneriler / Yol Haritası

- Test kapsamı artırılmalı ve servis katmanı için unit testler eklenmelidir  
- CI/CD süreci (lint, test, build) yapılandırılmalıdır  
- Input validation ve temel güvenlik iyileştirmeleri yapılmalıdır  
- Pagination eklenerek listeleme endpoint’leri iyileştirilmelidir  

---

## Sonuç

Proje genel olarak beklenen gereksinimleri karşılamaktadır.  
Eklenmesi veya Düzenlenmesi veya geliştirilmesi gereken bazı alanlar bulunmaktadır.  
Bu düzenlemeler yapıldığında proje daha düzenli ve kullanışlı hale gelecektir.


## Code Review Raporu 

Hazırlayan : Salih Kızılkaya Öğr no: 245172026

1-Mimari ve Teknoloji Yığını
Proje, Express.js tabanlı, Sequelize ORM kullanan ve SQLite/PostgreSQL desteği sunan
olgun bir yapıdadır. Önceki versiyonlara kıyasla daha kapsamlı bir veri modeline ve
dokümantasyona sahiptir.

Özellik Durum Gözlem
Veri Modeli ✅Mükemmel Ürünler, Sipariş Kalemleri ve Müşteriler arasındaki ilişkiler tam kurgulanmış.
Dokümantasyon ✅Mükemmel Swagger UI entegrasyonu yapılmış ve docs/ altında detaylı raporlar mevcut.
Hata Yönetimi ✅Başarılı Trace ID ve merkezi error handler ile tutarlı bir yapı sunulmuş.
Test Kapsamı ✅Başarılı Unit ve Integration testleri (Jest) ile edge case'ler kapsanmış.

2-Öne Çıkan Teknik Detaylar
Güçlü Yönler:
• Transaction Yönetimi: orderService.js içinde sipariş oluşturma işlemi
sequelize.transaction ile korunmuş. Stok düşümü ve sipariş kalemlerinin oluşturulması
atomik bir şekilde yapılıyor.
• Stok Takibi: Ürün bazlı trackStock kontrolü ve otomatik stok düşümü mekanizması iş
mantığına doğru entegre edilmiş.
• Gelişmiş ETL: import_customers_from_csv.js scripti, isim temizleme (cleanName), telefon
normalizasyonu ve duplicate kontrolü gibi gelişmiş veri temizleme adımları içeriyor.
• Middleware Kullanımı: traceMiddleware ve responseLogger ile her isteğin yaşam
döngüsü ve performansı izlenebilir hale getirilmiş.

3-Geliştirilmesi Gereken Alanlar:

• Validation Katmanı: Servis katmanında manuel if kontrolleri yerine Joi veya Zod
gibi bir kütüphane kullanılarak şema bazlı doğrulama yapılabilir.
• Hard-coded Değerler: Bazı scriptlerde ve servislerde hata mesajları veya varsayılan
değerler (örn: 'Bilinmeyen') hard-coded olarak yer alıyor; bunlar bir sabitler (constants)
dosyasına taşınabilir.
• Pagination: Müşteri listeleme ucu kayıt ile sınırlandırılmış ancak dinamik sayfalama
(page, limit) parametreleri tam olarak işlenmemiş.

4-Güvenlik ve Performans:

• Güvenlik: SQL Injection riskine karşı Sequelize parametreli sorguları kullanılıyor. Ancak
API uçlarında rate-limiting veya helmet gibi temel güvenlik middleware'leri eksik.
• Performans: SQLite kullanımı küçük ölçekli işler için idealdir; ancak findAll
sorgularında limit ve offset kullanımı büyük veri setleri için optimize edilmelidir.

5 Sonuç

mini-crm-main projesi, bir MVP (Minimum Viable Product) aşamasının ötesine geçmiş,
üretim ortamına (production) hazır özellikler barındıran kaliteli bir çalışmadır. Özellikle
Transaction ve Stok Yönetimi gibi kritik iş süreçlerinin doğru kurgulanmış olması projenin
en büyük artısıdır.

Öneriler:

. API Güvenliği: helmet ve cors paketleri eklenmeli.
. Şema Doğrulama: express-validator entegrasyonu ile input güvenliği artırılmalı.
. Frontend Hazırlığı: API response yapısı, frontend tarafında kolayca tüketilebilecek
şekilde (örn: data , meta , errors blokları) standartlaştırılmalı.


**UPDATE**

Tüm servisler test edilmiştir,
Github konfigürasyonu yapılmıştır.
İnceleme için teşekkürler.
- Burak Ünal


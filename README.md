ScoutAI ⚽🏀
Yapay Zeka Destekli Spor Maç Analizi ve Tahmin Platformu

ScoutAI, Sofascore API'yi kullanarak canlı maç verilerini, puan durumlarını, oyuncu istatistiklerini ve yapay zeka destekli maç tahminlerini tek bir HTML dosyasında sunan gerçek zamanlı bir spor zeka uygulamasıdır. Herhangi bir kurulum veya derleme adımı gerektirmez.

Özellikler
Canlı Maç Skorları — Futbol, basketbol ve tenis maçlarını gerçek zamanlı takip et. Herhangi bir maça tıklayınca gol, kart ve değişiklik detayları açılır
Maç Analizi ve Tahminler — İki takım adı gir, ScoutAI son 10 maç verisini çekerek şu tahminleri üretir: Maç Sonucu (MS1/MS0/MS2), Alt/Üst 2.5, KG Var/Yok, İY/MS, Handikap
Puan Durumu — Süper Lig, Premier Lig, La Liga, Bundesliga ve Serie A için güncel 25/26 sezon tabloları
Oyuncu Arama — İsim yazarak herhangi bir oyuncunun pozisyonunu, takımını ve piyasa değerini gör
Kupon Oluşturucu — Tahminleri kupona ekle, toplam oran, risk seviyesi ve güven skorunu takip et
Tahmin Geçmişi — Tahminleri kaydet, doğru/yanlış olarak işaretle ve isabet oranını izle
Kullanılan Teknolojiler
Teknoloji	Kullanım Amacı
Sofascore API (RapidAPI üzerinden)	Canlı skorlar, maç verileri, takım istatistikleri, puan durumu, oyuncu bilgileri
Chart.js	Gol form grafikleri, tahmin doğruluk grafikleri
Vanilla JS	Tüm uygulama mantığı — async/await, localStorage, DOM yönetimi
CSS Variables	Tam karanlık tema ve dinamik renk sistemi
HTML5	Tek dosya uygulama, framework yok, derleme adımı yok
Nasıl Çalıştırılır
Bu uygulama API istekleri yaptığı için HTTP üzerinden sunulması gerekir (file:// protokolüyle açılamaz).

Seçenek 1 — Python (önerilen):

cd scoutai-klasoru
python -m http.server 8080
# Tarayıcıda aç: http://localhost:8080/scoutai.html
Seçenek 2 — Hazır BAT dosyası (Windows):

BASLAT.bat dosyasına çift tıkla
Sunucu otomatik başlar ve tarayıcı açılır.

API Entegrasyonu
ScoutAI, RapidAPI üzerindeki Sofascore API ile entegre çalışır. Kullanılan endpoint'ler:

GET /search — Takım ve oyuncu arama
GET /teams/get-last-matches — Takım başına son 10 maç
GET /teams/get-next-matches — Yaklaşan maçlar
GET /tournaments/get-live-events — Spora göre canlı maç akışı
GET /tournaments/get-standings — 25/26 sezonu lig tablosu
GET /matches/get-incidents — Maç başına gol, kart ve değişiklikler
GET /categories/list-live — Aktif canlı kategoriler
Tüm API çağrıları merkezi bir api() fonksiyonu üzerinden async/await ile yapılır, hata yönetimi tek noktadan sağlanır.

Tahmin Modeli
Tahmin motoru, gerçek maç verilerine dayalı ağırlıklı bir puanlama formülü kullanır:

Takım Puanı = (Galibiyet × 3) + Beraberlik + (Ort. Gol × 2) − (Ort. Yenilen × 1.5)
Kazanma olasılığı göreceli takım puanlarından türetilir ve şu tahminlere dönüştürülür:

Maç sonucu (MS1/MS0/MS2)
Alt/Üst eşiği (ortalama gol sayısına göre)
KG Var/Yok (bireysel hücum gücüne göre)
İY/MS (kazanma olasılığından türetilir)
Handikap (puan farkına göre)
Lisans
MIT — özgürce kullan, değiştir ve dağıt.

Sofascore API + RapidAPI ile geliştirildi | Spor analitiği portföyleri için tasarlandı

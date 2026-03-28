
# ScoutAI ⚽🏀
### Gerçek Zamanlı Spor Analizi ve Tahmin Platformu

> Sofascore API'den canlı maç verisi çeken, takım istatistiklerini işleyen ve yapay zeka destekli maç tahminleri üreten tek dosyalık bir web uygulaması — tamamen vanilla JavaScript ile, framework kullanılmadan geliştirildi.

**[GitHub](https://github.com/d3xsz/scoutai)** | Geliştirici: [@d3xsz](https://github.com/d3xsz)

---

## Ne Yaptım ve Neden?

Gerçek bir API entegrasyonunu pratik bir kullanım senaryosuyla birleştiren bir şey geliştirmek istedim. Spor analitiği bunun için mükemmel bir alan oldu — asenkron veri çekme, ham istatistikleri anlamlı tahminlere dönüştürme ve framework kullanmadan dinamik bir arayüz oluşturmayı gerektirdi.

Ortaya çıkan şey, tek bir HTML dosyasında çalışan tam işlevsel bir spor zeka panosu oldu.

---

## Öne Çıkan Teknik Başarılar

- **7 Sofascore API endpoint** entegrasyonu — merkezi async handler ve hata yönetimi ile
- **Gerçek zamanlı maç olayları** — herhangi bir canlı maça tıklayınca gol, kart ve değişiklikler anında yüklenir
- **İstatistiksel tahmin modeli** — galibiyet oranları, gol ortalamaları ve H2H verilerinden 5 farklı bahis türü üreten özel ağırlıklı formül
- **localStorage kalıcılığı** — kupon oluşturucu ve tahmin geçmişi sayfa yenilenmesinde kaybolmaz
- **Dinamik DOM yönetimi** — framework yok, tüm arayüz güncellemeleri manuel innerHTML ile verimli şekilde yapılır
- **Sıfır derleme adımı** — tek HTML dosyası, local server ile her yerde çalışır

---

## Özellikler

| Özellik | Açıklama |
|---|---|
| Canlı Skorlar | Futbol, basketbol, tenis — tıklandığında gol/kart/değişiklik detayları |
| Maç Analizi | İki takım gir, MS1/MS0/MS2, Alt/Üst, KG, İY/MS, Handikap tahminleri al |
| Puan Durumu | 5 büyük lig için güncel 25/26 sezonu tabloları |
| Oyuncu Arama | İsimle arama, pozisyon, takım ve piyasa değeri bilgisi |
| Kupon Oluşturucu | Tahmin ekle, toplam oran, risk seviyesi ve güven skoru takip et |
| Tahmin Geçmişi | Kaydet, doğru/yanlış işaretle, isabet oranını grafikle izle |

---

## Teknoloji Yığını

```
Frontend  →  HTML5, CSS3 (custom properties, grid, flexbox), Vanilla JS (ES6+)
API       →  Sofascore / RapidAPI (REST, async/await, fetch)
Grafikler →  Chart.js
Depolama  →  localStorage
```

---

## Neler Öğrendim?

- Üçüncü taraf REST API'lerle çalışmak — kimlik doğrulama, rate limit ve hatalı yanıtları yönetmek
- Ham istatistik verisinden tahmin modeli oluşturmak
- Framework kullanmadan state yönetimi
- CORS sorunlarını debug etmek ve tarayıcı güvenlik politikalarını anlamak
- Iteratif problem çözme — canlı maç olayları özelliği tek başına 15'ten fazla debug döngüsü gerektirdi

---

## Nasıl Çalıştırılır?

```bash
git clone https://github.com/d3xsz/scoutai
cd scoutai
python -m http.server 8080
# Tarayıcıda aç: http://localhost:8080/scoutai.html
```

**Windows:** `BASLAT.bat` dosyasına çift tıkla — sunucu başlar ve tarayıcı otomatik açılır.

---

## Kullanılan API Endpoint'leri

```
GET /search                      Takım ve oyuncu arama
GET /teams/get-last-matches      Takım başına son 10 maç
GET /teams/get-next-matches      Yaklaşan maçlar
GET /tournaments/get-live-events Spora göre canlı maç akışı
GET /tournaments/get-standings   Lig tablosu (sezona özel ID'lerle)
GET /matches/get-incidents       Maç başına gol, kart, değişiklikler
GET /categories/list-live        Aktif canlı spor kategorileri
```

---

## Tahmin Formülü

```
takimPuani = (galibiyet x 3) + beraberlik + (ortGol x 2) - (ortYenilen x 1.5)
kazanmaOlasiligi = takimPuani / (evPuan + depPuan)
```

Olasılıklar şu tahminlere dönüştürülür: Maç Sonucu, Alt/Üst 2.5, KG Var/Yok, İY/MS, Handikap.

---

*MIT Lisansı*

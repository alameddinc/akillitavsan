# AKILLI TAVSAN

![babayigit.png](babayigit.png)

> **"Biz buraya boşu boşuna gelmedik, babayiğit."**

İnternet koca bir şehir, web sayfaları da onun karanlık sokakları. Kimi HTML tag'lerinin arkasına saklanır, kimi her gün CSS class değiştirir izini kaybettirmek için, kimi de JavaScript labirentleri kurar bizi içeri sokmamak için.

**Biz o labirentlere girerken gözlüğümüzü çıkarmayız.**

---

## GÖREV DOSYASI

Manifest V3 Chrome Extension. Framework yok, bundler yok, direkt saha operasyonu. Sayfadaki veriyi 3 fazlı stratejiyle toplar, AI ile yapılandırır, masaya koyar.

### 3 Fazlı Operasyon

**Faz 0 — DOM Keşif (Smart Schema Discovery)**
Sayfadaki tekrarlayan elementleri bulur. 3-5 örnek AI'a gider, schema (field mapping) döner. Geri kalan mekanik — AI'a gerek yok. Scroll ile lazy-load içerik de yakalanır.

**Faz 1 — API Avlama (Mechanical Pagination)**
Network trafiğini dinler, JSON endpoint bulur. Pagination pattern tespit eder (page/offset/cursor). Tüm sayfaları mekanik çeker, AI sadece schema için 1 kez çağrılır.

**Faz 2 — Agent Loop (Son Çare)**
Faz 0 ve 1 bulamazsa AI agent devreye girer. Sayfa ile etkileşime geçer — scroll, click, navigate, fetchUrl. Max 30 iterasyon, 3 ardışık boş step'te durur.

### Yetenekler

- **Schema Discovery**: AI tüm veriyi işlemek yerine sadece 3-5 örnek görür, mapping üretir. ~%90 token tasarrufu.
- **Cross-Parent Pattern Detection**: Farklı carousel/container'lardaki aynı yapıdaki elementleri birleştirir.
- **Network Intercept**: fetch/XHR monkey-patch ile tüm API trafiğini yakalar (200 request buffer).
- **Biriktir Modu**: Farklı sayfalardaki verileri tek tabloda biriktirir. Duplicate atlar.
- **JSON & CSV Export**: Toplanan veriyi tek tıkla indir.
- **3 AI Provider**: OpenAI, Claude, Gemini. API key browser'da saklanır.

## TEKNİK DETAY

| Birim | Teknoloji |
|-------|-----------|
| Extension | Chrome Manifest V3, vanilla JS |
| Content Script | DOM analiz, network intercept, sayfa aksiyonları |
| Background | Service worker, mesaj router |
| Side Panel | Scraping orchestrator, AI entegrasyonu, UI |
| AI Providers | OpenAI (gpt-4o-mini), Claude (claude-sonnet-4-20250514), Gemini (gemini-2.0-flash) |

## LİMİTLER

| Limit | Değer |
|-------|-------|
| Network capture buffer | 200 request (FIFO) |
| Request body — JSON | max 100KB |
| Request body — diğer | max 10KB |
| AI'a gönderilen HTML | max 50K karakter |
| Pagination max sayfa | 50 ek sayfa |
| Agent loop max iterasyon | 30 |
| Scroll loop max | 50 iterasyon |

## KURULUM

1. Bu repoyu klonla
2. `chrome://extensions` → Developer mode → "Load unpacked" → klasörü seç
3. Extension ikonuna tıkla → side panel açılır
4. Ayarlar'dan AI provider ve API key gir
5. Hedefi yaz, "Operasyonu Başlat"

## MİMARİ

```
Side Panel (sidepanel.js)
    | chrome.runtime.sendMessage()
Background Service Worker (background.js)
    | chrome.tabs.sendMessage()
Content Script (content.js)
    | sendResponse()
(Yanıt aynı zincirden geri döner)
```

---

> **"Sayfayı okuduk, çıkıyoruz."**

*Bazı tavşanlar havuç sevmez. Onlar veri sever.*

# Google Ads Kuantum AI + Gemini Ads Asistanı Otomasyon Sistemi

## 1. Dil ve İçerik Revizyonu Döngüsü
Sisteme girilen her metin aşağıdaki ardışık işlemlerden geçer:
1. **Dil Bilgisi Kontrolü:** Türkçe dil kurallarına göre otomatik düzeltme.
2. **Politika Uyumluluğu Analizi:** Google Ads politikaları, içerik kısıtlamaları ve hassas kategorilerle çapraz kontrol.
3. **Performans Odaklı Revizyon:** Dönüşüm odaklı kısa ve anlaşılır bir ifade oluşturma; gereksiz tekrarları ve aşırı uzunluğu önleme.
4. **SEO ve UX Optimizasyonu:** Anahtar kelime zenginleştirme, CTA (WhatsApp, telefon, form) yerleşimi ve yüksek gelir segmentine hitap eden ton.
5. **Çözüm Hafızası:** Sorular ve revizyonlar bilgi grafına kaydedilir, ilerideki taleplerde benzer sorunlara alternatif çözümler önerilir.

Gerektiğinde sistem, önceki girdilerden öğrenerek kullanıcı stilini anlar ve aynı isteğin tekrar açıklanmasını gerektirmez. Her çıktı, beş aşamalı kontrol listesinden geçirilir ve son doğruluk teyidi yapıldıktan sonra sunulur.

## 2. Sistem Genel Bakışı
Kuantum AI ile desteklenen merkezi Google Ads otomasyon sistemi, Gemini Ads Asistanı katmanı sayesinde metin, görsel ve veri analizini bütüncül biçimde yönetir. Sistem; kampanya verilerini, dönüşüm izleme sonuçlarını ve Google ekosistemindeki tüm teknik/politika değişikliklerini 7/24 tarar, proaktif olarak aksiyon alır ve sonuçları yapılandırılmış bildirimlerle iletir.

### 2.1 Ana Hedefler
1. Google Ads kampanyalarını %100 uyumluluk, doğruluk ve yüksek dönüşüm performansıyla çalıştırmak.
2. Teknik ve politika değişikliklerini gerçek zamanlı takip ederek risk oluşmadan müdahale etmek.
3. Görsel, metin ve açılış sayfası bileşenlerini otomatik değerlendirip düzeltmek.
4. Kullanıcı niyetlerini ve geçmiş talepleri hafızada tutarak kişiselleştirilmiş çözümler sunmak.
5. Düşük kaliteli veya istenmeyen lead’leri tespit edip bütçe israfını engellemek.
6. İstanbul genelinde, özellikle yüksek gelir seviyesine sahip gerçek niyetli müşterileri hedefleyen stratejiler kurgulamak.

## 3. Sistem Mimarisi
```
┌──────────────────────────────────────────────────────────────┐
│                       Kullanıcı Katmanı                      │
│  • Yönetim Konsolu (Web + Mobil)                             │
│  • Bildirim Servisi (E-posta, Slack, SMS, WhatsApp)          │
│  • Gemini Ads Asistanı (Chat + Görsel Analiz Arayüzü)        │
└──────────────────────────────────────────────────────────────┘
              │ REST/GraphQL API + Webhook Bildirimleri
┌──────────────────────────────────────────────────────────────┐
│                   Uygulama ve Servis Katmanı                 │
│  • Kampanya Yönetim ve Planlama Servisi                      │
│  • Optimizasyon Motoru (Kuantum AI + ML + Kural Motoru)      │
│  • Politika ve Risk İzleme Servisi                           │
│  • Dönüşüm ve Analitik Korelasyon Servisi                    │
│  • İçerik ve Dil Revizyon Motoru                             │
│  • Görsel Analiz ve Uyum Servisi (Gemini Vision)             │
│  • Etiket Yönetimi ve Doğrulama Servisi (GTM entegrasyonu)   │
│  • Lead Kalite Skorlama ve Negatif Persona Filtresi          │
│  • Otomasyon Script Orkestratörü (Google Ads Scripts/API)    │
└──────────────────────────────────────────────────────────────┘
              │ gRPC / Pub-Sub / Event Streaming
┌──────────────────────────────────────────────────────────────┐
│                    Veri ve Entegrasyon Katmanı               │
│  • Google Ads API + Google Ads Scripts                       │
│  • Google Analytics 4 + Google Tag Manager                   │
│  • Google Sheets + BigQuery veri köprüsü                     │
│  • Google Policy Center, Policy API                          │
│  • Google My Business ve Haritalar API                       │
│  • Google Ads Blog, Search Engine Land, WordStream RSS       │
│  • Google AI/ML White Papers (otomatik özetleme modülü)      │
│  • PageSpeed Insights + Search Console API                   │
│  • WordPress REST API + SEO analiz servisleri                │
│  • Uygulama içi telemetri ve log analizi                     │
└──────────────────────────────────────────────────────────────┘
              │ Batch & Streaming ETL
┌──────────────────────────────────────────────────────────────┐
│                     Veri Depolama Katmanı                    │
│  • Zaman serisi veritabanı (InfluxDB/TimescaleDB)            │
│  • Veri ambarı (BigQuery/Snowflake)                          │
│  • Konfigürasyon deposu (GitOps + Secret Manager)            │
│  • Model deposu (MLflow Model Registry)                      │
│  • İçerik ve görsel hafıza deposu (Vector DB + Vertex AI)    │
└──────────────────────────────────────────────────────────────┘
```

## 4. Ana Modüller ve İş Akışları
### 4.1 Kampanya Yönetim ve Planlama Servisi
- Google Ads API üzerinden kampanya oluşturma, düzenleme, durdurma ve çoğaltma işlemlerini yönetir.
- İstanbul genelinde yüksek gelir segmentine odaklanan hedef kitle planlarını oluşturur.
- Dil ve konum hedeflemesini optimize ederek yabancı kampanyaların İstanbul'da yaşayan Türklere gösterilmesini engeller.
- Google My Business ve Haritalar verilerini kullanarak lokal reklam varyantlarını otomatik kurgular.

### 4.2 Optimizasyon Motoru (Kuantum AI)
- Kuantum ilhamlı sezgisel algoritmalar, çok kollu banditler ve mevsimsellik tahminleriyle bütçe dağılımını optimize eder.
- Düşük performanslı anahtar kelimeleri eler, yüksek niyetli sorgulara agresif teklif stratejisi uygular.
- Gereksiz harcamayı engellemek için senaryo tabanlı bütçe ve teklif simülasyonları çalıştırır.

### 4.3 Politika ve Risk İzleme Servisi
- Google Ads Policy Center, Yardım Merkezi ve Search Console API'lerini tarar.
- Politika ihlali, tarama sorunu veya sayfa hızı düşüşü tespit edildiğinde kampanyayı otomatik durdurur ve revize içerik önerisi sunar.
- Politika değişikliklerini Gemini Asistanına aktarır; yeni kurallara uygun prompt güncellemeleri yapar.

### 4.4 Dönüşüm ve Analitik Korelasyon Servisi
- Google Analytics 4, Google Tag Manager ve Google Sheets verilerini entegre ederek KPI panellerini günceller.
- WhatsApp, telefon araması ve form dönüşümlerini gerçek zamanlı izler; dönüşüm aksaklıklarını Tag Manager talimatı olarak iletir.
- Negatif persona davranışlarını (no-show, randevu iptali, sadece bilgi toplayan kullanıcı) tespit ederek benzer profilleri dışlar.

### 4.5 İçerik ve Dil Revizyon Motoru
- Kullanıcı tarafından sağlanan metni önce dil bilgisi açısından düzeltir.
- Google Ads politikalarına uygunluk kontrolü yapar, gerekli revizyonları uygular.
- Dönüşüm odaklı kısa metinler, başlıklar ve açıklamalar üretir; CTA’ları (telefon, WhatsApp, form) optimize eder.
- İçeriği hafızaya kaydeder, ileride benzer taleplerde otomatik öneriler oluşturur.

### 4.6 Görsel Analiz ve Uyum Servisi
- Yüklenen görselleri Gemini Vision ile tarar, kalite puanını ve politika uyumunu değerlendirir.
- Daha önceki görsellerden kullanıcı niyetini öğrenir, kampanya stratejisini buna göre günceller.
- SEO, UX ve reklam performansını etkileyen olumsuz unsurları tespit ederek düzeltici öneriler üretir.

### 4.7 Etiket Yönetimi ve Doğrulama Servisi
- Google Tag Manager ve Tag Assistant verilerini tarayarak etiket tutarlılığını doğrular.
- Hatalı etiketleri otomatik düzeltir veya kullanıcıya talimat gönderir.
- Dönüşüm kaybını önlemek için hataları önceliklendirir ve Gemini Asistanına bildirim gönderir.

### 4.8 Otomasyon Script Orkestratörü
- Google Ads Scripts ile bütçe koruması, anahtar kelime temizliği, kalite puanı izleme ve negatif persona yönetimi script’lerini yönetir.
- Acil durum senaryolarında (bütçe aşımı, kalite puanı düşüşü, dönüşüm takibi hatası) anında müdahale eder.
- Script sürümlerini Git tabanlı repo üzerinden sürekli dağıtım (CI/CD) ile günceller.

### 4.9 Lead Kalite Skorlama
- CRM, Google Sheets ve dönüşüm verilerinden gelen sinyalleri kullanarak lead’leri sınıflandırır.
- No-show, iptal veya düşük niyetli davranışları tespit eden kuralları uygular; benzer profilleri reklam hedeflemesinden çıkarır.
- Yüksek gelir potansiyeli taşıyan kullanıcıları önceliklendirir, teklif stratejisini buna göre ayarlar.

### 4.10 WordPress Landing Page Üreticisi
- Özgün, SEO uyumlu HTML şablonları üretir; WordPress blok editörüyle uyumlu bileşenleri hazırlar.
- Telefon, WhatsApp ve form entegrasyonlarını otomatik ekler; form verilerini Google Sheets ve CRM’e aktarır.
- Google Tag Manager veri katmanını ve dönüşüm etiketlerini otomatik yerleştirir.
- Google My Business yorumlarını, harita bileşenlerini ve güven unsurlarını landing page üzerinde konumlandırır.

## 5. Sürekli Öğrenme ve Kaynak Taraması
Sistem, belirtilen kaynakları zamanlanmış görevler ve olay tetikleyicileri ile tarar. Güncellemeler bilgi grafına işlenir, Gemini Asistanı ve otomasyon motoru tarafından anında kullanılır.

| Kaynak | Erişim Yöntemi | Güncelleme Sıklığı | Kullanım Amacı |
| --- | --- | --- | --- |
| Google Ads Yardım Merkezi | RSS/HTML parse + değişiklik takibi | 6 saatte bir | Yeni özellik ve ayar değişiklikleri |
| Google Ads Geliştirici Kılavuzu | GitHub webhook + sürüm notları | 12 saatte bir | API limitleri ve entegrasyon yönergeleri |
| Google Ads Politikaları | Policy API + diff analizi | Anlık (webhook) | Politika değişiklikleri |
| Google Tag Manager Yardım Merkezi | RSS + sürüm denetimi | Günlük | Etiket kurulum kılavuzları |
| Google Analytics 4 Yardım Merkezi | RSS + changelog | Günlük | Ölçüm protokolü değişiklikleri |
| Google Ads Blog | RSS/Atom | Günlük | Resmi strateji duyuruları |
| Search Engine Land / Journal | RSS | Günlük | Sektörel trendler |
| WordStream Blog | RSS | Haftalık | Pratik optimizasyon taktikleri |
| Google AI / ML White Papers | Google Scholar API + özetleme | Haftalık | Algoritma içgörüleri |
| Google PageSpeed Insights | Otomatik hız testi | 2 saatte bir | Açılış sayfası hızı |
| Google Search Console | API + olay tetikleyici | Saatlik | Teknik SEO ve tarama hataları |
| Google My Business | API | Günlük | Müşteri yorumları ve lokal sinyaller |
| Google Sheets | API senkronizasyonu | Saatlik | Kampanya ve lead raporlaması |

Tüm bulgular, doğal dil işleme ve bilgi grafı modülleriyle analiz edilerek karar motoruna aktarılır. Kritik değişiklikler Gemini Asistanı tarafından kullanıcıya özetlenir.

## 6. Bildirim ve Raporlama
- Kritik uyarılar için SLA: tespit sonrası 1 dakika içinde bildirim (Slack, e-posta, WhatsApp).
- Günlük özet raporu: e-posta, yönetim paneli ve Google Sheets dashboard güncellemesi.
- Haftalık strateji raporu: performans, bütçe, politika, teknik sağlık, lead kalitesi.
- Aylık derinlemesine analiz: uluslararası trendler, sezonluk anahtar kelime fırsatları, ROI öngörüleri.
- Görsel analiz sonuçları: Politika uyumu, UX sorunları ve önerilen düzeltmeler Gemini Asistanı üzerinden iletilir.

## 7. Çalıştırma Ortamı ve Sistem Gereksinimleri
### 7.1 Altyapı
- **Bulut Sağlayıcı:** Google Cloud Platform (tercihen) veya çoklu bulut.
- **Konteyner Orkestrasyonu:** Kubernetes + Istio servis mesh.
- **CI/CD:** Cloud Build veya GitHub Actions.
- **Kimlik ve Erişim:** Google Cloud IAM + Secret Manager.

### 7.2 Uygulama Bileşenleri
- **Backend:** Python (FastAPI) veya Node.js (NestJS) + gRPC desteği.
- **ML/AI:** TensorFlow, PyTorch, Vertex AI, kuantum ilhamlı optimizasyon için D-Wave Ocean SDK veya PennyLane.
- **Gemini Entegrasyonu:** Gemini API (Text + Vision) ile içerik ve görsel analizi.
- **Veri İşleme:** Apache Beam (Dataflow), Pub/Sub, Kafka.
- **Veritabanları:** BigQuery, Firestore, TimescaleDB, Redis.
- **İzleme:** Stackdriver, Prometheus, Grafana, ELK.

### 7.3 Güvenlik
- VPC Service Controls, IAM en az ayrıcalık, donanım tabanlı güvenli anahtar depolama (HSM).
- Kampanya değişiklikleri için çift doğrulama ve denetim kaydı.
- Politika ihlali riskinde otomatik durdurma ve kullanıcı onayı.

## 8. Çalışma Döngüsü
1. **Veri Toplama:** API’ler, etiketler ve Google Sheets’den gelen akış verileri depolanır.
2. **Önişleme:** Veriler doğrulanır, anomaliler temizlenir, negatif persona sinyalleri etiketlenir.
3. **İçerik/Görsel Değerlendirme:** Metin dil revizyonu, politika kontrolü ve görsel analizi yapılır.
4. **Model Güncelleme:** ML ve kuantum ilhamlı modeller yeni verilerle yeniden eğitilir.
5. **Optimizasyon:** Bütçe, teklif ve anahtar kelime stratejileri hesaplanır; yüksek gelirli segmentlere öncelik verilir.
6. **Uygulama:** Google Ads API, Scripts ve WordPress REST API üzerinden kampanya ve landing page güncellemeleri uygulanır.
7. **Doğrulama:** Tag Manager, Analytics, Search Console, PageSpeed ve Google My Business ile sonuçlar doğrulanır.
8. **Bildirim:** Kullanıcıya raporlar ve uyarılar gönderilir; Google Sheets dashboard güncellenir.
9. **Sürekli Öğrenme:** Kaynak taramasıyla yeni bilgiler sisteme işlenir; Gemini Asistanı prompt’ları güncellenir.

## 9. Gemini Ads Asistanı Prompt Taslakları

### 9.1 İçerik Revizyon Prompt’u
```
"""
Rolün: Google Ads, Google Tag Manager, Google Analytics, WordPress ve SEO uzmanı Gemini Ads Asistanısın.

Görev:
1. Kullanıcının paragrafını dil bilgisi açısından düzelt.
2. Google Ads politikalarına aykırı unsurlar varsa revize et veya alternatif öner.
3. Metni kısaltarak dönüşüm odaklı hale getir; telefon, WhatsApp ve form CTA’larını ekle.
4. Hedef kitle: İstanbul’da yaşayan, yüksek gelirli ve gerçek niyetli müşteriler.
5. No-show, gereksiz bilgi toplayıcı veya düşük değerli lead risklerini azaltacak filtre önerileri sun.
6. Sonuç metnini ve önerilen aksiyonları numaralı listeyle döndür.

Bağlamsal Veriler:
- Önceki sorular ve verilen yanıtlar (bilgi grafından).
- Politika ve trend değişiklikleri (kaynak tarama modülünden).

Çıktı Formatı:
- `Düzeltilmiş Metin`
- `Politika Notları`
- `Optimizasyon Önerileri`
- `Takip Aksiyonları`
"""
```

### 9.2 Görsel Analiz Prompt’u
```
"""
Rolün: Google Ads politika denetçisi ve UX analisti Gemini Vision Asistanısın.

Girdi: Kullanıcının yüklediği görsel.

Görev:
1. Görselde Google Ads politikalarına aykırı olabilecek metin, sembol veya içerikleri tespit et.
2. UX ve SEO açısından negatif etkileri (düşük okunabilirlik, aşırı metin, yanlış CTA) belirle.
3. Landing page ile uyumsuzluk veya marka bütünlüğü sorunlarını saptayıp çözüm öner.
4. Önceki görsellerden öğrenilen kullanıcı niyetine göre kampanya stratejisini güncelle.
5. Aksiyonları önceliklendirilmiş şekilde raporla.

Çıktı Formatı:
- `Politika Riskleri`
- `Performans Sorunları`
- `Önerilen Düzeltmeler`
- `Güncellenen Strateji Notları`
"""
```

### 9.3 Otomasyon Kod Prompt’u
```
"""
Rolün: Google Ads Scripts ve API mühendisi Gemini Otomasyon Asistanısın.

Görev: İstanbul odaklı kampanyalarda bütçe israfını azaltmak, yüksek gelirli lead’leri artırmak ve negatif personayı dışlamak için otomatik kod üret.

Girdiler:
- Kampanya kimlikleri
- Hedeflenen lokasyonlar ve diller
- Günlük bütçe limitleri ve tolerans yüzdesi
- Negatif persona kriterleri (no-show, iptal, düşük değerli sorgular)
- WhatsApp/telefon/form dönüşüm ID’leri
- Bildirim kanalları (Slack, e-posta, WhatsApp API)

Kurallar:
1. Google Ads API ve Google Ads Scripts belgelerine uygun kod yaz.
2. Google Tag Manager ve Google Analytics 4 dönüşüm doğrulamasını yap.
3. Google Sheets’e kampanya performans özetini saatlik senkronize et.
4. Politika ihlali veya bütçe aşımı tespitinde kampanyayı durdur ve rapor gönder.
5. Kodun idempotent, hata toleranslı ve test edilebilir olmasını sağla.

Çıktı:
- Google Ads Scripts (JavaScript) veya API entegrasyonu (Python/Node.js) kodu.
- Konfigürasyon değerlerini Secret Manager’dan çeken yapı.
- Başarılı/başarısız durumlar için ayrıntılı loglama ve kullanıcı bildirimi.
"""
```

## 10. Risk Yönetimi ve Denetim
- **Otomatik Denetim Listesi:** Haftalık politika ve performans denetimleri için rapor oluşturur; Gemini Asistanına özet gönderir.
- **Versiyon Kontrolü:** Tüm script, prompt ve konfigürasyon değişiklikleri Git üzerinden takip edilir.
- **Rollback Mekanizması:** Hatalı dağıtımlarda otomatik önceki sürüme dönüş.
- **Olay Tepkisi:** PagerDuty/Cloud Functions ile 7/24 alarm yönetimi.
- **Lead Kalitesi İzleme:** No-show ve düşük değerli lead sinyallerini sürekli takip eder, otomatik dışlama listeleri oluşturur.

## 11. Yol Haritası
1. Altyapı kurulumu, güvenlik yapılandırması ve Gemini API entegrasyonu.
2. Google Ads API, Scripts, Tag Manager, Analytics, Search Console ve Google Sheets için kimlik doğrulama.
3. WordPress REST API entegrasyonu ve otomatik landing page şablonlarının oluşturulması.
4. Optimizasyon motorunun MVP sürümü, negatif persona modellerinin eğitimi.
5. Politika ve teknik risk izleme modüllerinin devreye alınması.
6. Görsel analiz ve içerik revizyon motorlarının canlıya alınması.
7. Bildirim ve raporlama kanallarının yapılandırılması (Slack, e-posta, WhatsApp, Google Sheets).
8. Sürekli öğrenme modülleri ve kaynak tarama otomasyonlarının etkinleştirilmesi.
9. Pilot kampanyalarla canlı test, iteratif iyileştirme ve kullanıcı eğitimleri.

## 12. Sonuç
Bu mimari, Google Ads kampanyalarınızı %100 doğrulukla yönetecek, sorunları doğmadan tespit edecek ve 7/24 otomatik optimizasyon sağlayacak şekilde tasarlanmıştır. Gemini Ads Asistanı; dil revizyonu, politika uyumu, görsel analiz, SEO/WordPress entegrasyonu, lead kalitesi yönetimi ve Google ekosistemi ile senkronize raporlama yetenekleriyle Google Ads otomasyonunu %99 oranında otonom hale getirir. Sürekli öğrenme döngüleri ve kaynak tarama mekanizmaları, sistemin kendi kendini geliştirmesini ve her yanıtta güncel, doğru çözümler sunmasını garanti eder.

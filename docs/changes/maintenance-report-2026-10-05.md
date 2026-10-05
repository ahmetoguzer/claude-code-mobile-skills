# Bakım Turu #12 — 2026-10-05

Kalıcı oturuma bağlı Routine, cron ile zamanında ateşlendi; `docs/MAINTENANCE.md`
prosedürü uygulandı.

Tur sayısı: 12 (**hem 4'e hem 12'ye bölünüyor** → yönlendirme evali **ve** derin
tutarlılık denetimi bu turda birlikte çalıştırıldı).

## Taranan kaynaklar (§1)

AGP, Compose/Navigation/CameraX/Credential Manager, Hilt/coroutines/Retrofit/KSP
(4 WebFetch doğrulaması), Play Console politikası, Xcode/Swift/App Store Connect,
`android/skills` (ilk kez §1b'nin kalıcı parçası olarak) — 6 WebSearch sorgusu +
4 WebFetch.

## §2a — Version catalog tam geçişi

| Giriş | Mevcut | Sonuç |
|---|---|---|
| `agp` | 9.4.0 | En güncel, değişiklik yok |
| `kotlin` | 2.4.20 | En güncel, değişiklik yok |
| `ksp` | 2.3.12 | En güncel (WebFetch ile doğrulandı), değişiklik yok |
| `composeBom` | 2026.08.00 | En güncel, değişiklik yok |
| `hilt` | 2.60.1 | En güncel (WebFetch ile doğrulandı), değişiklik yok |
| `coroutines` | 1.11.0 | En güncel (WebFetch ile doğrulandı), değişiklik yok |
| `retrofit` | **2.12.0 → 3.0.0** | **Güncellendi** — bkz. aşağı |

## Bulgular ve değişiklikler

| Bulgu | Kaynak | Aksiyon |
|---|---|---|
| Retrofit'in kendi sürüm notları: **3.x, 2.x ile forward binary-uyumlu** | github.com/square/retrofit/releases (WebFetch) | İki tur önce "major bump, riskli" diye ertelenen Retrofit 3.0.0 artık güvenli olduğu doğrulanarak uygulandı. Tek pratik fark: OkHttp artık Kotlin'de yazılı (4.12), transitive Kotlin bağımlılığı geliyor |
| Navigation 2.9.8 stable | AndroidX sürüm sayfaları | `android-navigation`/`android-gradle-build` sürüm pinlemiyor — aksiyon gerekmedi |
| Play Console: 28 Ekim 2026'da izin kısıtlaması (daha dar veri erişimi); 1 Ekim'den itibaren alternatif billing ücret raporlama | Play Console duyuruları | İzin kısıtlaması henüz detaylandırılmamış (genel), billing konusu mimari kapsamımız dışında — her ikisi de aksiyon gerektirmedi |
| `android/skills`: son otomatik güncelleme 25 Eylül (bot PR #210), Ekim'e özgü yeni bir skill/desen değişikliği bulunamadı | github.com/android/skills | İlk kez §1b'nin kalıcı parçası olarak tarandı — sağlıklı, değişiklik yok |

## Yönlendirme evali (§4c, her 4. tur)

31 skill'in description'ları yalnızca okunarak 58 vaka değerlendirildi:
**58/58 geçti.** `on-device-ai`'nin yeni ADK tetikleyicileri ("AI agent", "ajan
mimarisi", "tool calling", "ADK") hiçbir mevcut vakayla çakışmadı — tur #4 ve
#8'deki sonuçla birebir aynı.

## Derin tutarlılık denetimi (§4c, her 12. tur) — İLK KOŞUM

`mobile-code-review`'in "Skill / Doküman PR'ları" checklist'i kullanılarak tüm
koleksiyon çapraz tarandı:

- **Hata yönetimi deseni** (`runCatching` vs `try/catch`) — 9+6 dosyada her ikisi
  de var, spot-check edildi: çelişki değil, meşru farklı bağlamlar (ör.
  `android-data-layer`'daki `try` kullanımı `RemoteMediator.load()`'ın sabit
  framework imzasından geliyor, `runCatching` kullanılamaz)
- **Hand-off referansları** — mevcut `devret` cümleleri tarandı, hedef skill'lerin
  hepsi var (kopuk referans yok)
- **Katalog tutarlılığı** — 3 katalog arasında (`README.md`, `skills/README.md`,
  `templates/CLAUDE.md`) `validate.sh` zaten senkron doğruluyor, ama **satır
  içeriği** eşleşmesi elle kontrol edildi:
  - 🔴 **Bulundu:** `skills/README.md`'de `on-device-ai` satırı hâlâ eski
    açıklamayı taşıyordu ("ML Kit, Gemini Nano, özel model, hibrit cihaz-bulut")
    — ADK eklendiğinden beri (tur #10) güncellenmemiş. **Düzeltildi.**
  - 🔴 **Bulundu:** `on-device-ai`'nin description'ındaki yeni "ajan mimarisi"
    tetikleyicisinin `android-architect`'in genel "mimari" kapsamına karşı hiçbir
    sınır notu yoktu — koleksiyondaki diğer komşu-alan skill'lerin hepsinde bu
    desen var, burada eksikti. **Düzeltildi** — "ajan" burada AI agent
    orkestrasyonu anlamına geldiğini, genel mimarinin android-architect'e
    devredildiğini açıklayan bir cümle eklendi.
- **ARCHITECTURE.md** — `on-device-ai`/`android-gradle-build` ile ilgili
  bölümler yüksek seviyeli (kutu diyagramı, örnek yönlendirme tablosu),
  spesifik içerik iddiası taşımıyor — güncelleme gerekmedi

## Doğrulama (§3)

```
./scripts/validate.sh   → 31 skill, 0 hata, 0 uyarı
./scripts/check-links.sh → 73 link, 0 kırık
```

## Sonuç

1 doğrulanmış sürüm güncellemesi (Retrofit 3.0.0) + 2 derin denetim düzeltmesi
(stale catalog satırı, eksik hand-off sınırı) + yönlendirme evali 58/58.
`docs/maintenance-log.md`'ye ayrı commit ile işlenecek.

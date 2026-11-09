# Bakım Turu #17 — 2026-11-09

Kalıcı oturuma bağlı Routine, cron ile zamanında ateşlendi; `docs/MAINTENANCE.md`
prosedürü uygulandı.

Tur sayısı: 17 (4'e ve 12'ye bölünmüyor → periyodik görev yok).

## Taranan kaynaklar (§1)

AGP, Compose/Navigation/CameraX, Kotlin/Hilt/coroutines/Retrofit/KSP, Play
Console politikası, Xcode/Swift/App Store Connect, `android/skills` — 6
WebSearch sorgusu + 3 WebFetch doğrulaması (AGP 9.5.0, Kotlin 2.4.21, KSP
uyumluluğu).

## §2a — Version catalog tam geçişi

| Giriş | Mevcut | Sonuç |
|---|---|---|
| `agp` | **9.4.0 → 9.5.0** | **Güncellendi** — Gradle 9.6.0 minimum gerektiriyor, not eklendi |
| `kotlin` | **2.4.20 → 2.4.21** | **Güncellendi** — bug-fix release, KSP uyumluluğu doğrulandı |
| `ksp` | 2.3.12 | En güncel ve 2.4.21 ile uyumlu (sorun bulunamadı), değişiklik yok |
| `composeBom` | 2026.09.00 | En güncel (Compose 1.12.1 hâlâ stable, 1.13.0-rc01 henüz değil), değişiklik yok |
| `hilt` | 2.60.1 | En güncel (WebFetch ile doğrulandı), değişiklik yok |
| `coroutines` | 1.11.0 | Önceki turlarda doğrulandı, bu tur tekrar kontrol edilmedi | 
| `retrofit` | 3.0.0 | En güncel (WebFetch ile doğrulandı), değişiklik yok |

## Bulgular ve değişiklikler

| Bulgu | Kaynak | Aksiyon |
|---|---|---|
| **AGP 9.5.0 stable** yayınlandı (Ekim 2026) — Gradle minimum sürümü 9.6.0'a yükseldi | developer.android.com/build/releases/agp-9-5-0-release-notes (WebFetch) | `android-gradle-build/SKILL.md` güncellendi, Gradle wrapper uyarısı eklendi |
| **Kotlin 2.4.21** (bug-fix release, 8 Ekim 2026) | kotlinlang.org/docs/releases.html (WebFetch) | Güncellendi; KSP 2.3.12 ile uyumluluk sorunu bulunamadı (google/ksp#2964 tarzı bir regresyon yok) |
| Navigation 3 1.2.1'de **compileSdk 37'den 36'ya düşürülmüş** (4 Kasım) | AndroidX sürüm notları | Hiçbir skill Navigation sürümü pinlemiyor — aksiyon gerekmedi, ama tuhaf bir geri alma, izlemeye değer |
| CameraX compileSdk 37 gereksinimi yeniden teyit edildi | AndroidX sürüm notları | Zaten tutarlı (compileSdk 37 iki tur önce set edildi) |
| Play Console: trader status beyanı (Kasım 2026'dan itibaren, AB/UK tüketici hukuku, tam tarih 1 Şubat 2027), Local Network izni kısıtlaması (API 37+) | Play Console duyurusu (29 Ekim) | İş/yasal beyan süreci, mimari kapsamımız dışında — aksiyon gerekmedi. Local Network kısıtlaması hiçbir skill'de referanslı değil, izlemeye değer |
| Xcode 27.2 stable, App Store Connect 3.3.1 | Apple duyuruları | `ios-swift-architect` sürüm pinlemiyor — aksiyon gerekmedi |
| `android/skills`: düzenli otomatik güncellemeler devam ediyor, bizimle örtüşen bir değişiklik yok | github.com/android/skills | Sağlıklı |

## Doğrulama (§3)

```
./scripts/validate.sh   → 31 skill, 0 hata, 0 uyarı
./scripts/check-links.sh → 73 link, 0 kırık
```

## Sonuç

2 doğrulanmış, kaynak linkli sürüm güncellemesi (AGP 9.5.0, Kotlin 2.4.21).
`docs/maintenance-log.md`'ye ayrı commit ile işlenecek.

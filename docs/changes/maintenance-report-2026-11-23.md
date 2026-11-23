# Bakım Turu #19 — 2026-11-23

Kalıcı oturuma bağlı Routine, cron ile zamanında ateşlendi; `docs/MAINTENANCE.md`
prosedürü uygulandı.

Tur sayısı: 19 (4'e ve 12'ye bölünmüyor → periyodik görev yok).

## Taranan kaynaklar (§1 / §1b)

AGP, Compose/Navigation/CameraX, Kotlin/Hilt/coroutines/Retrofit/KSP, Play
Console politikası, Xcode/Swift/App Store Connect — 6 WebSearch sorgusu;
`android/skills` — commit geçmişi + `agp-9-upgrade` skill'i doğrudan
WebFetch ile incelendi; Compose BOM/Compose sürüm sayfaları ve KSP/Kotlin
release sayfaları WebFetch ile doğrulandı.

## §2a — Version catalog tam geçişi

| Giriş | Mevcut | Sonuç |
|---|---|---|
| `agp` | 9.5.1 | Güncel, değişiklik yok |
| `kotlin` | 2.4.21 | Güncel (resmi sayfa doğrulandı, 2.5.0 Aralık 2026'ya planlı) |
| `ksp` | 2.3.14 | Güncel (resmi sayfa doğrulandı, yeni regresyon yok) |
| `composeBom` | **2026.09.00 → 2026.11.01** | **Güncellendi** — Compose 1.13.0 artık stable (18 Kasım, resmi sürüm tablosu doğrulandı) |
| `hilt` | 2.60.1 | Güncel, değişiklik yok |
| `coroutines` | 1.11.0 | Güncel, değişiklik yok |
| `retrofit` | 3.0.0 | Güncel, değişiklik yok |

## Bulgular ve değişiklikler

| Bulgu | Kaynak | Aksiyon |
|---|---|---|
| **Compose 1.13.0 stable** oldu (animation/foundation/material/runtime/ui), BOM 2026.11.01'e karşılık geliyor | developer.android.com/jetpack/androidx/releases/compose (WebFetch) | `android-gradle-build/SKILL.md`: `composeBom` 2026.09.00 → 2026.11.01 |
| `android/skills`'te 15 Kasım'da büyük bir toplu senkronizasyon (#279, 154 dosya) — AGP 9 upgrade, Compose, navigation, security, testing, on-device AI skill'lerini kapsıyor | github.com/android/skills commit geçmişi (WebFetch) | `agp-9-upgrade` skill'i doğrudan incelendi: bizim catalog'umuzun zaten önünde olduğu doğrulandı (KSP≥2.3.6, Hilt≥2.59.2 gereksinimleri bizdekinden daha düşük), yeni bir AGP/Gradle minimum sürümü belirtilmiyor — aksiyon gerekmedi. Not: bu skill KMP projelerini desteklenmiyor olarak işaretliyor, bizim kapsamımızı etkilemiyor |
| Play Console: Kasım 2026'da yeni bir duyuru bulunamadı; bilinen tarihler (26 Ağustos targetSdk, 27 Ocak 2027 contacts/location zorunlu uyum) değişmedi | Play Policy sayfaları | Aksiyon gerekmedi |
| Xcode/Swift: Kasım 2026'ya özel resmi bir not bulunamadı; App Store Connect'te yaş derecelendirme açıklayıcıları (16 Kasım) ve Sandbox grup satın alma testi eklendi | developer.apple.com duyuruları | `ios-swift-architect` sürüm pinlemiyor — aksiyon gerekmedi |

## Doğrulama (§3)

```
./scripts/validate.sh   → 31 skill, 0 hata, 0 uyarı
./scripts/check-links.sh → 73 link, 0 kırık
```

## Sonuç

1 doğrulanmış, kaynak linkli sürüm güncellemesi (Compose BOM 2026.11.01).
`docs/maintenance-log.md`'ye ayrı commit ile işlenecek.

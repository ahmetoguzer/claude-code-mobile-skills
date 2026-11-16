# Bakım Turu #18 — 2026-11-16

Kalıcı oturuma bağlı Routine, cron ile zamanında ateşlendi; `docs/MAINTENANCE.md`
prosedürü uygulandı.

Tur sayısı: 18 (4'e ve 12'ye bölünmüyor → periyodik görev yok).

## Taranan kaynaklar (§1)

AGP, Compose/Navigation/CameraX, Kotlin/Hilt/coroutines/Retrofit/KSP, Play
Console politikası, Xcode/Swift/App Store Connect, `android/skills` — 6
WebSearch sorgusu + 2 WebFetch doğrulaması (AGP 9.5.1 sürüm sayfası, KSP
release notları).

## §2a — Version catalog tam geçişi

| Giriş | Mevcut | Sonuç |
|---|---|---|
| `agp` | **9.5.0 → 9.5.1** | **Güncellendi** — "Current Release" (WebFetch ile doğrulandı) |
| `kotlin` | 2.4.21 | Güncel, değişiklik yok |
| `ksp` | **2.3.12 → 2.3.14** | **Güncellendi** — bkz. aşağıdaki kritik bulgu (google/ksp#3286) |
| `composeBom` | 2026.09.00 | Güncel, değişiklik yok |
| `hilt` | 2.60.1 | Güncel, değişiklik yok |
| `coroutines` | 1.11.0 | Güncel, değişiklik yok |
| `retrofit` | 3.0.0 | Güncel, değişiklik yok |

## Bulgular ve değişiklikler

| Bulgu | Kaynak | Aksiyon |
|---|---|---|
| **Kritik — KSP 2.3.13 regresyonu**: paralel KSP task çalıştırmalarında Hilt aggregating module binding'leri (ve diğer library sembolleri) sessizce düşüyor; build hatasız geçer ama DI runtime'da kırık çıkar. 2.3.14 (13 Kasım) düzeltiyor | `github.com/google/ksp/releases` (WebFetch) — google/ksp#3286 | `android-gradle-build/SKILL.md`: `ksp` 2.3.12 → 2.3.14 doğrudan atlandı (2.3.13'e hiç uğranmadı), kalıcı "ASLA kullanma" uyarısı eklendi |
| **AGP 9.5.1** "Current Release" olarak işaretli (9.6.0 henüz alpha, aksiyon gerektirmiyor) | developer.android.com/reference/tools/gradle-api (WebFetch) | `android-gradle-build/SKILL.md`: `agp` 9.5.0 → 9.5.1 |
| `android/skills`: düzenli otomatik güncellemeler devam ediyor, bizimle örtüşen bir değişiklik yok | github.com/android/skills | Sağlıklı |
| Play Console, Xcode/App Store Connect: bu tur yeni, aksiyon gerektiren bir duyuru yok | Resmi duyuru sayfaları | Aksiyon gerekmedi |

## Doğrulama (§3)

```
./scripts/validate.sh   → 31 skill, 0 hata, 0 uyarı
./scripts/check-links.sh → 73 link, 0 kırık
```

## Sonuç

2 doğrulanmış, kaynak linkli sürüm güncellemesi (AGP 9.5.1, KSP 2.3.14).
KSP 2.3.14 güncellemesi özellikle önemli: repo hiçbir zaman kırık 2.3.13'e
maruz kalmadı (2.3.12'den doğrudan 2.3.14'e atlandı), ama bu bulgu ileride
hiçbir tur ya da insan okuyucunun o sürüme basmasını önlüyor.
`docs/maintenance-log.md`'ye ayrı commit ile işlenecek.

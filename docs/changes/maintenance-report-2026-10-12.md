# Bakım Turu #13 — 2026-10-12

Kalıcı oturuma bağlı Routine, cron ile zamanında ateşlendi; `docs/MAINTENANCE.md`
prosedürü uygulandı.

Tur sayısı: 13 (4'e ve 12'ye bölünmüyor → periyodik görev yok).

## Taranan kaynaklar (§1)

AGP, Compose/Navigation/CameraX, Kotlin/Hilt/coroutines/Retrofit/KSP, Play
Console politikası, Xcode/Swift/App Store Connect, `android/skills` — 6
WebSearch sorgusu + 2 WebFetch doğrulaması (Compose BOM, kotlinx.coroutines).

## §2a — Version catalog tam geçişi

| Giriş | Mevcut | Sonuç |
|---|---|---|
| `agp` | 9.4.0 | En güncel, değişiklik yok |
| `kotlin` | 2.4.20 | En güncel, değişiklik yok |
| `ksp` | 2.3.12 | En güncel/eşleşen, değişiklik yok |
| `composeBom` | **2026.08.00 → 2026.09.00** | **Güncellendi** |
| `hilt` | 2.60.1 | En güncel, değişiklik yok |
| `coroutines` | 1.11.0 | En güncel (WebFetch ile doğrulandı), değişiklik yok |
| `retrofit` | 3.0.0 | En güncel, değişiklik yok |

## Bulgular ve değişiklikler

| Bulgu | Kaynak | Aksiyon |
|---|---|---|
| Compose 1.12.1 (bug-fix release) yayınlandı, BOM 2026.09.00 ona karşılık geliyor | mvnrepository.com, developer.android.com per-library sürüm tablosu | `android-gradle-build/SKILL.md`: `composeBom` güncellendi |
| Navigation 3 stable 1.2.0 | AndroidX sürüm sayfaları | Hiçbir skill pinlemiyor — aksiyon gerekmedi |
| AGP hâlâ 9.4.0 (en güncel); AGP 10.0 "late 2026" olarak yol haritasında, tarih belirsiz | AGP roadmap | İzlemeye devam, aksiyon gerekmedi |
| Play Console contacts/location izin kısıtlaması için **çelişkili tarih**: resmi Policy Deadlines sayfası 27 Ocak 2027 diyor, bazı üçüncü parti bloglar 28 Ekim 2026 diyor | Play Console Help (resmi) vs. üçüncü parti bloglar | **Teyit edilemedi** — hiçbir skill'de bu konuya dair pinlenmiş tarih yok, MAINTENANCE.md §0 kuralı gereği dokunulmadı. Resmi kaynak esas alınmalı (27 Ocak 2027); gelecek bir turda netleşirse işlenir |
| Xcode 27.1 RC, App Store Connect yeni store özellikleri (asset library, canlı önizleme) | Apple duyuruları | `ios-swift-architect` sürüm pinlemiyor — aksiyon gerekmedi |
| `android/skills`: Ekim'e özgü net bir bulgu yok — repo'nun kendi Actions sayfasında "Revert last skills update" (PR #126) görünüyor ama detay doğrulanamadı | github.com/android/skills | Sağlıklı tarama, somut aksiyon gerektiren bir şey bulunamadı — sessiz hafta, sağlığın kanıtı |

## Açık, ele alınmayan standing item

Yok — `android/skills` artık standing değil, kalıcı §1b taraması (tur #12'den
beri).

## Doğrulama (§3)

```
./scripts/validate.sh   → 31 skill, 0 hata, 0 uyarı
./scripts/check-links.sh → 73 link, 0 kırık
```

## Sonuç

1 doğrulanmış, kaynak linkli sürüm güncellemesi (Compose BOM 2026.09.00).
`docs/maintenance-log.md`'ye ayrı commit ile işlenecek.

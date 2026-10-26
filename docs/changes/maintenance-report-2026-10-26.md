# Bakım Turu #15 — 2026-10-26

Kalıcı oturuma bağlı Routine, cron ile zamanında ateşlendi; `docs/MAINTENANCE.md`
prosedürü uygulandı.

Tur sayısı: 15 (4'e ve 12'ye bölünmüyor → periyodik görev yok).

## Taranan kaynaklar (§1)

AGP, Compose/Navigation/CameraX/Credential Manager, Kotlin/Hilt/coroutines/
Retrofit/KSP, Play Console politikası, Xcode/Swift/App Store Connect,
`android/skills` — 6 WebSearch sorgusu.

## Bulgular ve değişiklikler

| Bulgu | Kaynak | Aksiyon |
|---|---|---|
| **İki tur süren Play Console izin tarihi belirsizliği çözüldü** — çelişki değil, iki ayrı kilometre taşıymış: Play Console 27-28 Ekim 2026'dan itibaren contacts/location iznini submission öncesi **uyarı** olarak işaretliyor; tam **zorunlu** uyum tarihi 27 Ocak 2027. Birden fazla bağımsız kaynak bu iki tarihli yapıda birleşiyor | Play Console Help, apppresser.com, helpnetsecurity.com, vioside.com (çapraz doğrulandı) | `android-security/SKILL.md` §7'ye eklendi — mevcut Photo Picker/COARSE location rehberliğinin doğal devamı olarak |
| AGP hâlâ 9.4.0 (stable), 9.4.1 iddiası bu tur da doğrulanamadı — gerçek değil | AGP resmi sürüm sayfaları | Aksiyon gerekmedi |
| Compose 1.13.0-beta02, Navigation 3 1.3.0-alpha03, CameraX 1.7.0-rc01 — hepsi pre-release | AndroidX sürüm sayfaları | Stable değil, pinlenen sürümlere etki yok |
| Xcode 27.2 RC, App Store Connect güncellemeleri (Xcode Cloud taşındı, TestFlight 4.4.1) | Apple duyuruları | `ios-swift-architect` sürüm pinlemiyor — aksiyon gerekmedi |
| `android/skills`: PR #249 (21 Ekim) dahil düzenli otomatik güncellemeler devam ediyor, bizimle örtüşen bir değişiklik bulunamadı | github.com/android/skills | Sağlıklı, aksiyon gerekmedi |

## §2a — Version catalog

Bu tur yeni bir sürüm bulgusu yok (tüm pre-release/beta); `android-gradle-build`
catalog'u geçen turda zaten tam doğrulanmıştı, bu tur dokunulmadı.

## Doğrulama (§3)

```
./scripts/validate.sh   → 31 skill, 0 hata, 0 uyarı
./scripts/check-links.sh → 73 link, 0 kırık
```

## Sonuç

1 yeni içerik eklendi (`android-security`'ye contacts/location izin politikası)
— iki tur süren "teyit edilemedi" durumunu kapatıyor. `docs/maintenance-log.md`'ye
ayrı commit ile işlenecek.

# Wiki Index — Hermes Agent

> Bu dosya wiki'nin kategori bazlı içerik kataloğudur. Yeni sayfa eklendikçe güncellenir.

---

## Günlükler

- [[2026-05-21]] — Hermes bellek keşfi, plugin mimarisi, X ajan tweet paylaşım sistemi
- [[2026-05-22]] — Ekrem ilk otomatik tweet'ler, Sheets entegrasyonu, Ayla keşfi, pipeline testleri, X API krizi
- [[2026-05-25]] — Hermes cron: Sheets'ten Zero Click tweeti atildi
- [[2026-05-24]] — LLM Wiki entegrasyonu, Osman Gundem raporu
- [[2026-05-23]] — Pipeline hata analizi, Ekrem yeniden yapılanma, tweet havuzu, X API kredisi geldi
- [[hafıza]] — 3 günlük özet: API key'ler, yapılandırmalar, kararlar, blocker'lar

## En Yeni Güncellemeler

- **2026-05-23**: [[hafıza]] — 3 günlük konuşma özeti ve hafıza kaydı
- **2026-05-23**: [[2026-05-23]], [[2026-05-22]], [[2026-05-21]] — Günlük sayfaları oluşturuldu
- **2026-05-23**: [[007-pipeline-hata-cozumleri]] — Pipeline hata analizi ve çözümleri
- **2026-05-23**: [[ayla-gorsel-uretim]] — Ayla görsel üretim wiki sayfası
- **2026-05-23**: [[hermes-infografik-pipeline]] — İnfografik pipeline wiki sayfası
- **2026-05-23**: [[ekrem-tweet-havuzu]] — Tweet havuzu sistemi
- **2026-05-23**: [[ekrem-x-ajani]] — Ekrem v4.0 (Musti çıktı, havuz eklendi)

## Sources (Kaynak Özetleri)

- [hermes-agent-genel-bakis](sources/hermes-agent-genel-bakis.md) — Hermes Agent'in temel ozellikleri, mimarisi, LLM saglayicilari
- [autoresearch-genel-bakis](sources/autoresearch-genel-bakis.md) — Karpathy'nin otonom arastirma sistemi
- [hermes-control-interface-genel-bakis](sources/hermes-control-interface-genel-bakis.md) — HCI v3.4.0 web dashboard

## Entities (Varlıklar)

### Sistem
- [hermes-agent](entities/hermes-agent.md) — Temel Hermes Agent entity
- [hermes-api](entities/hermes-api.md) — API entity ve endpoint'leri
- [hermes-dashboard](entities/hermes-dashboard.md) — Dashboard service entity
- [hermes-router](entities/hermes-router.md) — Faz 1 API routing servisi
- [paperclip](entities/paperclip.md) — Paperclip entity ve özellikleri
- [telegram-bot](entities/telegram-bot.md) — Telegram bot entity
- [cmo-dashboard](entities/cmo-dashboard.md) — CMO Dashboard entity
- [vps-server](entities/vps-server.md) — VPS sunucu ve Coolify entegrasyonu
- [hermes-control-interface](entities/hermes-control-interface.md) — HCI entity ve kurulumu

### Botfusions Ajanları
|- [osman-arastirma](entities/osman-arastirma.md) — Osman araştırma ajanı 🔍
|- [ekrem-x-ajani](entities/ekrem-x-ajani.md) — Ekrem X algoritma ajanı
- [ekrem-tweet-havuzu](entities/ekrem-tweet-havuzu.md) — Tweet konuları havuzu
- [ayla-gorsel-uretim](entities/ayla-gorsel-uretim.md) — Ayla görsel analiz ve üretim ajanı
- [ayla-analizleri](entities/ayla-analizleri.md) — Ayla görsel analiz arşivi
- [hermes-infografik-pipeline](entities/hermes-infografik-pipeline.md) — Otomatik infografik pipeline
- [botfusions-x-tweet-arsivi](entities/botfusions-x-tweet-arsivi.md) — Botfusions X tweet arşivi

- [[osman-arastirma]] — Osman araştırma ajanı
## Concepts (Kavramlar)

- [ajan-ogrenme-dongusu](concepts/ajan-ogrenme-dongusu.md) — Kapali ogrenme dongusu
- [hermes-wiki-butunlesme](concepts/hermes-wiki-butunlesme.md) — Wiki → Hermes entegrasyonu
- [hermes-memory-arsivi](concepts/hermes-memory-arsivi.md) — Agent memory dump → wiki arşivi
- [dashboard-patterns](concepts/dashboard-patterns.md) — Dashboard tasarım örüntüleri
- [deployment-stratejisi](concepts/deployment-stratejisi.md) — Dağıtım stratejisi
- [multi-agent-yonetimi](concepts/multi-agent-yonetimi.md) — Çoklu ajan yönetimi
- [hermes-orchestrator-gelisim-plani](concepts/hermes-orchestrator-gelisim-plani.md) — Master gelisim plani: 5 faz, open/closed specialists, 5 kaynak arastirmasi

## Decisions (Kararlar)

- [001-windows-wsl2-mi-yerel-mi](decisions/001-windows-wsl2-mi-yerel-mi.md) — Windows native vs WSL2
- [002-telegram-entegrasyonu](decisions/002-telegram-entegrasyonu.md) — Telegram gateway
- [003-vps-deployment-stratejisi](decisions/003-vps-deployment-stratejisi.md) — VPS deployment
- [004-self-improvement-dongusu](decisions/004-self-improvement-dongusu.md) — SOUL.md ve self-improvement
- [005-dashboard-plugins](decisions/005-dashboard-plugins.md) — Dashboard plugin yapısı
- [006-hermes-control-interface-degerlendirmesi](decisions/006-hermes-control-interface-degerlendirmesi.md) — HCI değerlendirmesi
- [007-pipeline-hata-cozumleri](decisions/007-pipeline-hata-cozumleri.md) — Pipeline hata analizi
- [008-x-ban-koruma-plani](decisions/008-x-ban-koruma-plani.md) — X API ban koruma, kill switch, OAuth 1.0a uploadMedia
- [009-memory-wiki-arsiv-kurali](decisions/009-memory-wiki-arsiv-kurali.md) — Memory %80'de wiki'ye arşivleme kuralı

## Issues (Sorunlar)

- [001-windows-pwd-modul-hatasi](issues/001-windows-pwd-modul-hatasi.md) — Windows'da pwd modulu bulunamadi
- [002-windows-cli-encoding](issues/002-windows-cli-encoding.md) — cli.py prompt_toolkit Win32 console hatasi

## Syntheses (Sentezler)

- [sprint-context](syntheses/sprint-context.md) — Genel proje bağlamı ve yol haritası
- [teknik-mimari](syntheses/teknik-mimari.md) — Hermes Agent teknik mimari
- [entegrasyon-akisi](syntheses/entegrasyon-akisi.md) — Sistem entegrasyonları

## Archive (Arsiv)

- [archived-decisions](archive/archived-decisions.md) — Eski ve geçersiz kararlar

- [[osman-arastirma]] -- Osman arastirma ajani
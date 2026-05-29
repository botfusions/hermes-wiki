# Wiki Log — Hermes Agent

> Append-only zaman damgali olay kaydi. En yeni olay en ustte.

## [2026-05-29 18:03] cron | Ekrem X Ajani — 29 May 18:00

- **Tweet 33:** AI Yönetişimi 2026 (88/100 🔥) — Databricks + Google Cloud + Salesforce sentezi
- **3 LIKE:** alexgroberman (AI 42% ROI), nateherk (10x AI OS), alexgroberman (MS ChatGPT Guide)
- **1 REPOST:** shannholmberg (Hermes Agent specialist design)
- **3 yorum hazırlandı:** shannholmberg (#100), nateherk (#101), alexgroberman (#102)
- Queue güncellendi, header refresh

## [2026-05-26] create | Faz 2 Closed Workflows

- Workflow engine olusturuldu (workflows/engine.py, models.py)
- SEO raporu template'i eklendi (workflows/templates/seo-report.yaml) — 3 adimli pipeline
- Natural language cron scheduler eklendi (scheduler/parser.py, manager.py, routes.py)
- Turkce zaman ifadeleri → cron expression (9 pattern: gunluk, haftalik, aylik, interval, vb.)
- Router'a entegre edildi: GET /v1/workflows, POST /v1/workflows/{name}/run, POST /v1/schedule
- APScheduler + croniter + pytz dependency'leri eklendi
- VPS deploy: build + recreate basarili, endpoint'ler dogrulandi

## [2026-05-26] create | Hermes Router Faz 1

- hermes-router/ servisi olusturuldu (router.py, intent.py, agents.py, config.yaml)
- docker-compose.vps.yml'e router servisi eklendi (port 8699, router.turklawai.com)
- Wiki sayfasi olusturuldu: entities/hermes-router.md
- Faz 1: Temel Routing — API giris noktasi + intent detection + proxy

## [2026-05-26] create | Master gelisim plani + 5 kaynak arastirmasi

- hermes-orchestrator-gelisim-plani.md olusturuldu (concepts/)
- 5 kaynak degerlendirmesi kaydedildi (kullanici tanimi, Akshay, Nainsi, Kanika, scraping araclar)
- Crawl4AI ve Scrapegraph AI gelisim planina eklendi
- Browser Use zaten var — atlandi
- 5 fazlik yol haritasi: Routing → Closed Workflows → Orkestrasyon → Otonomi → Kanal Genisleme
- index.md guncellendi

| Tarih | Olay | Detay |
|-------|------|-------|
| 2026-05-26 | decision-009 | Memory → Wiki arşiv kuralı oluşturuldu: %80 dolunca wiki'ye taşı. Zep + Wiki + yerel memory hiyerarşisi tanımlandı. |
| 2026-05-25 | hermes-cron-1800 | Ekrem X ajani calisti (18:06 TSI). Gemini 3.5 Flash GA tweeti atildi (2058974214409908414, skor:84). 2 yeni tweet kuyruga eklendi (Salesforce AI trends). RT: @NousResearch Hermes Agent Jam, @GoogleDeepMind AlphaProof Nexus. Yorumlar hazir: @alexgroberman Google SEO, @nateherk AI trust. 11 hesap tarandi. |
| 2026-05-23 | ekrem-cron-3 | Ekrem cron job (16:00 UTC) — Google AI Overviews SEO tweeti atildi (ID: 2058216904020361422, skor: 84/100). Kill switch: 3/12. Havuz guncellendi: 1 bekleyen konu kaldi. |
| 2026-05-23 | osman-arastirma | Osman arastirma ajani olusturuldu: entities/osman-arastirma.md, skill scripts/skills/osman-arastirma.md, scripts/osman-calistir.py. Cron: 0 3,10 * * * (09:00/13:00 TSI). Tweet arsivi otomatik kayit eklendi (pipeline + Ekrem). |
| 2026-05-23 | pipeline-v3 | Pipeline v3 deploy: OAuth 1.0a media upload + tweet, kill switch (12/gun, 1h interval). Script: scripts/hermes-x-pipeline-v3.py. Cron: 0 9,11 * * *. post-tweet.py scripti Ekrem icin yazildi. Ekrem cron kill switch entegrasyonu eklendi. |
| 2026-05-23 | x-ban-koruma-plani | X API ban koruma plani olusturuldu: decisions/008-x-ban-koruma-plani.md. Kill switch, duplicate kontrol, OAuth 1.0a uploadMedia, gunluk limit. |
| 2026-05-23 | gunluk-sayfalari | 3 gunluk konusmalar wikiye kaydedildi: gunluk/2026-05-21.md, gunluk/2026-05-22.md, gunluk/2026-05-23.md. Hafiza ozeti: gunluk/hafiza.md |
| 2026-05-23 | pipeline-hata-analizi | Tum pipeline hatalari analiz edildi wikiye kaydedildi: decisions/007-pipeline-hata-cozumleri.md. Ekrem skillinne ogrenilmis dersler eklendi. |
| 2026-05-23 | infografik-pipeline-wiki | Infografik pipeline wiki sayfasi olusturuldu: entities/hermes-infografik-pipeline.md. API key sorunu var (Google AI Studio key gecersiz) |
| 2026-05-23 | ayla-wiki-sayfasi | Ayla gorsel uretim yetenekleri wiki sayfasi olusturuldu: entities/ayla-gorsel-uretim.md |
| 2026-05-23 | ekrem-guncelleme | Ekrem v4.0 — gunde 3 tarama (06:00/13:00/18:00 TSI) + havuz + tweet dongusu. Musti devre disi. Yeni sayfa: entities/ekrem-tweet-havuzu.md |
| 2026-05-22 | ayla-gorsel-ajani | Ayla — gorsel analiz ve olusturma ajani egitildi. Skill: scripts/skills/ayla-gorsel-ajani.md. Gemini 3.5 Flash vision ile calisir, OpenRouter API kullanir. Wiki sayfasi: entities/ayla-analizleri.md. |
| 2026-05-22 | botfusions-tweet-arsivi | @botfusionss hesabindaki tum tweetler entities/botfusions-x-tweet-arsivi.md sayfasina kaydedildi. 13 tweet bugun. Ekrem otomatik + manuel ayrimi yapildi. |
| 2026-05-22 | hci-inceleme-tamam | xaspx/hermes-control-interface kapsamli degerlendirme tamamlandi — 8 sayfa dashboard, RBAC, chat, token analizi, enterprise ozellikler, GO karari verildi |
| 2026-05-22 | dashboard-telafi-mecanismi | Mevcut dashboard ile HCI tamamlayici sistem olarak degerlendirildi — kaynak etkisi minimal, enterprise ozellikleri ekleniyor |
| 2026-04-22 | hci-inceleme | xaspx/hermes-control-interface v3.4.0 incelendi — web dashboard: 8 sayfa, RBAC, chat, token analizi, terminal |
| 2026-04-22 | hci-deploy-plan | HCI ayri konteyner/systemd olarak VPS'e eklendi, deployment planina 7 adim olarak yazildi |
| 2026-05-24 | llm-wiki-entegrasyon | Karpathy LLM Wiki skill'i aktif edildi. SCHEMA.md olusturuldu. raw/ klasoru eklendi. Wiki yapisi llm-wiki skill'i ile uyumlu hale getirildi. |

## [2026-05-24] ingest | Osman Gundem Raporu

- Tip: gundem (Firecrawl + DeepSeek)
- Kaynak: OpenRouter Firecrawl (5 sorgu)
- Analiz: DeepSeek (Kimi K2.6 fallback)
- Rapor: 2026-05-24-1749-gundem.md
- Havuz: 7 yeni fikir eklendi
- One cikan: Google May 2026 Core Update, Agentic AI, AI Kreatif Patlamasi
## [2026-05-29] cron | Ekrem X ajani calismasi (15:30 TSİ) — CreditsDepleted

- **Durum:** X API kredisi bitik — tüm xurl işlemleri bloke (whoami çalıştı)
- **Görev 1 (Queue):** Tweet 28 post edilemedi — kuyrukta bekliyor
- **Görev 2 (Tarama):** 12 hesap taranamadı — kredi yok
- **Görev 3 (Yeni Tweet):** Databricks State of AI Agents tweet'i hazırlandı (88/100) → kuyruğa eklendi (Tweet 31)
- **Görev 4 (Yorum):** 2 yeni yorum hazırlandı (#95 ModestMitkus, #96 NousResearch)
- **Görev 5 (Freshness):** Tüm ID'ler unique — tekrar yok
- **Kuyruk:** 27 posted + 4 bekleyen (Tweets 28-31)
- **Yorum dosyası:** 96 yorum hazır, manuel gönderim bekliyor

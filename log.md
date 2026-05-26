# Wiki Log — Hermes Agent

> Append-only zaman damgali olay kaydi. En yeni olay en ustte.

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

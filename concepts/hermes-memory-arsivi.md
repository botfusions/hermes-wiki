---
title: Hermes Memory Arşivi
tags: [memory, arşiv, sistem-bilgisi]
date: 2026-05-26
status: active
brain: A
---

# Hermes Memory Arşivi

Agent'in yerel memory'sinden wiki'ye taşınan kalıcı bilgiler. Agent her açılışta Zep Cloud'dan ve wiki'den okur, yerel memory sadece oturum içi için kullanılır.

## Model Sıralaması

| Sıra | Sağlayıcı | Model | Kullanım |
|------|-----------|-------|----------|
| 1. | DeepSeek | deepseek-v4-pro | **Default** — tüm işlemler |
| 2. | OpenRouter | google/gemini-3.5-flash | **Fallback** — DeepSeek düşerse |
| 3. | KIE.AI | claude-opus-4-7 | **Emergency** — sadece özel durumda |

**Not:** Vision/görsel okuma — DeepSeek desteklemez. Görsel analizi için OpenRouter üzerinden `google/gemini-3.5-flash` kullanılır.

## X/Twitter Hesabı

- **Hesap:** @botfusionss — Botfusions AI Reklam Ajansı
- **Plan:** X Premium+ (25.000 karakter limiti)
- **Kural:** KISA TWEET ATMA. 800-2000 karakter. Thread atma, show more = dwell time.
- **Auth:** xurl OAuth 1.0a ile VPS'te yapılandırıldı

## Ajanlar

### Ekrem — Canlı X Ajanı
- Cron: `0 3,6,9,12,15,18 * * *` (06:00-21:00 TSİ, 6 sefer)
- Görev: Tweet kuyruğundan sırayla alır, atar, [x] işaretler
- Kuyruk kaynağı: Osman raporu + Sheet pipeline
- İnsanı tempo: 09:00-22:00 TSİ, 30dk+ ara, günlük max 10-15 tweet
- Sheet pipeline (job `8246db66b706`): ayrı çalışır, günde 2 infografikli tweet (12:00/14:00 TSİ)
- Yorum formatı: Türkçe yorum + altına İngilizce çeviri
- **Önemli:** 403 hatası — X API mention'sız reply'i bloklar, sadece RT çalışır

### Ayla — Görsel Analiz + Oluşturma
- Model: `gemini-3.1-flash-image-preview` (Google AI Studio, genai SDK)
- API Key: `AIzaSyA447FaxxmPvjouCEj19KRhbV-43nFCwrI`
- ⚠️ **BAKİYE SIFIR:** 429 RESOURCE_EXHAUSTED — kredi yüklenmeden çalışmaz

### Osman — Araştırma Ajanı
- Cron: `0 3,10 * * *` (06:00/13:00 TSİ)
- Araçlar: Brave Search (ayda 2000 ücretsiz sorgu) + X Search (xAI/Grok 4.3) ile @shannholmberg, @swyx taraması
- Analiz: `moonshot-v1-auto` (BYOK)
- Maliyet: ~$0.06/rapor
- Script: `/opt/data/scripts/osman_cron_runner.py`
- **Not:** Kimi K2.6 reasoning modeli 90s timeout sorunu çıkardı → `moonshot-v1-auto`'ya dönüldü
- **Kimi API key:** `sk-YgKSw5wQDU0ZrvbPp1gVmT7BzezWic5ZqWPNopwqA4xG4gsY`

## Pipeline Kuralları

| Durum | Yapılacak |
|-------|-----------|
| DeepSeek invalid → | template fallback |
| Gemini invalid → | FAL.ai fallback |
| timezone hatası → | fix |
| FLUX/FAL Türkçe metin → | Python Pillow ile elle çiz (okuyamaz) |
| Baoyu da | yasak |

## xurl Medya Upload
```bash
xurl media upload --category tweet_image  # gerekli
# default amplify_video hata verir
```

## Saat Dilimi
Tüm zamanlar **TSİ** (Türkiye Saati, UTC+3). Asla UTC değil. Cron işlerinde TSİ → UTC dönüşümü otomatik yapılır.

## Kullanıcı Bilgisi
- **İsim:** Ömer Cenk Tokgöz (X: @botfusionss)
- **Email:** cenk.tokgoz@gmail.com
- **Tercih:** Türkçe iletişim
- **Not:** "Her şey kendi içinde bir sistem" prensibi benimsenir

## NotebookLM MCP Durumu
- MCP sunucu `notebooklm-mcp@2.0.0` kurulu
- Windows'ta `setup_auth` başarılı ✅
- Windows profili VPS'e kopyalandı ama Chromium versiyon farkı nedeniyle `authenticated: false` ❌
- VPS'te Chromium kurulu (148.0.7778.96) ama headless QR kodu gösteremiyor
- **Sonuç:** Hermes native MCP client desteklemiyor, Windows'ta HTTP bridge gerekli

## Related

- [[sprint-context]]
- [[ekrem-x-ajani]]
- [[osman-arastirma-ajani]]
- [[ayla-gorsel-ajani]]
- [[notebooklm-entegrasyonu]]

## Sources

- Hermes Agent Persona (sistem prompt'u)
- Oturum memory dump (26 May 2026)

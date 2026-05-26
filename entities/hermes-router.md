---
title: Hermes Router
tags: [router, orkestrasyon, api, faz-1]
date: 2026-05-26
status: active
brain: A
---

# Hermes Router

Faz 1 orkestrasyon servisi. Tek API giris noktasindan gelen mesaji intent detection ile dogru agent'a route eder.

## Port

8699

## Endpoint'ler

- `POST /v1/route` — Intent detection (hangi agent'a gidecek?)
- `POST /v1/chat/completions` — Proxy mode (dogru agent'a forward + response)
- `GET /health` — Router + tum agent'larin health durumu
- `X-Hermes-Agent` header — Manuel agent secimi

## Mimari

```
Kullanici -> Router (8699) -> Intent Detection -> Agent API -> Response
```

## Intent Detection

1. Keyword matching (hizli) — turkce karakter normalizasyonu
2. LLM fallback (DeepSeek) — confidence < 0.3 oldugunda
3. Default: CMO (belirsiz mesajlar)

## Konfigürasyon

`config.yaml` uzerinden agent tanimlari, keywords, defaults.

## Deployment

- Docker konteyner (docker-compose.vps.yml)
- Traefik: router.turklawai.com
- Network: agency-net + coolify

## Related

- [[hermes-orchestrator-gelisim-plani]]
- [[hermes-agent]]
- [[hermes-api]]

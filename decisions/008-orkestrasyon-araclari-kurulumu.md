---
title: Orkestrasyon Araclari Kurulumu
tags: [maestro, skill-factory, camel, orkestrasyon, kurulum]
source: tools/
date: 2026-05-22
status: active
brain: A
---

# Orkestrasyon Araclari Kurulumu

## Ozet

2026-05-22 tarihinde 3 orkestrasyon araci kuruldu/deg erlendirildi:

### 1. Maestro v0.102.0 — Multi-Agent Conductor
- **Durum**: KURULDU
- **Konum**: `tools/maestro/` (lokal) + PATH'te (`AppData/Local/Programs/maestro/`)
- **Ne yapar**: Misyon bazli coklu-ajan yonetimi, gorev dagitimi, eldegocme (handoff), sozlesmeler (contracts), Mission Control TUI
- **Entegrasyon**: Claude Code MCP server olarak kaydedildi
- **Komutlar**:
  - `maestro init` — proje konfigurasyonu
  - `maestro conduct` — conductor modu
  - `maestro mission` — misyon yonetimi
  - `maestro install` — skill'leri agent'lara senkronize et

### 2. Skill Factory — Meta-Skill
- **Durum**: KURULDU
- **Konum**: `~/.hermes/skills/meta/skill-factory/SKILL.md` + `~/.hermes/plugins/skill_factory.py`
- **Ne yapar**: Session'lari gozlemler, tekrarlanan is akislarini algilar, otomatik SKILL.md + plugin.py olusturur
- **Aktivasyon**: VPS'te `hermes skills reload` + `hermes skills enable skill-factory`
- **Komutlar**:
  - `/skill-factory propose` — yeni skill onerisi
  - `/skill-factory status` — durum kontrolu
  - `/skill-factory list` — skill listesi

### 3. Agent Camel — CaMeL Trust Boundaries
- **Durum**: GO (Kosullu) — Kurulum degerlendirildi, entegrasyon onaylandi
- **Konum**: `tools/hermes-agent-camel/` (kaynak kod)
- **Ne yapar**: Runtime trust boundary sistemi — monitor/enforce modlarinda agent guvenligi
- **Benchmark**: Enforce modda 3/3 saldiri bloke edildi
- **Entegrasyon**: Cherry-pick yapilabilir (2035 satir, ~30 nokta, 5-7 saat)
- **Oneri**: Once monitor modda basla, 1-2 hafta sonra enforce'a gec

## VPS Uzerinde Yapilmasi Gerekenler

```bash
# 1. Skill Factory aktivasyonu
hermes skills reload
hermes skills enable skill-factory

# 2. Maestro skill olarak kurulum (opsiyonel)
cd /opt/data && maestro install

# 3. Agent Camel monitor modda baslatma (gelecek)
# hermes --camel-guard monitor
```

## Bildirim Mesaji (Hermes icin)

Asagidaki mesaj Hermes'e SOUL.md uzerinden veyaTelegram bot uzerinden iletilebilir:

---

**Hermes Agent Bilgilendirme — 2026-05-22**

Yeni orkestrasyon aracları sisteme eklendi:

1. **Maestro**: Artık misyon bazlı çoklu-ajan koordinasyonu yapabilirsin. `maestro` komutu PATH'te. Misyon oluştur, görevleri dağıt, handoff yap.

2. **Skill Factory**: Tekrarlayan iş akışlarını otomatik algılayıp skill'e dönüştüren meta-skill aktif. `/skill-factory propose` ile manuel tetikleyebilirsin.

3. **Agent Camel**: CaMeL güvenlik guard değerlendirmesi tamamlandı. İlk aşamada monitor modda güvenlik izlemesi yapılacak. Enforce moduna geçiş planlanıyor.

Kullanıma hazır: `maestro --help`, `/skill-factory status`

---

## Related

- [[007-agent-camel-degerlendirmesi]] — Agent Camel detayli degerlendirme
- [[006-hermes-control-interface-degerlendirmesi]] — HCI degerlendirmesi
- [[self-improvement-loop]] — Self-improvement mekanizmasi

---
title: Agent Camel CaMeL Guard Degerlendirmesi
tags: [camel, guvenlik, degerlendirme, karar]
source: tools/hermes-agent-camel
date: 2026-05-22
status: active
brain: B
---

# Agent Camel CaMeL Guard Degerlendirmesi

## Nedir?

CaMeL Guard, Hermes Agent icin gelistirilmis bir **runtime trust boundary** (guven siniri) sistemidir. Temel amaci, AI ajaninin **güvenilmeyen veri kaynaklari** (tool outputlari, web sayfalari, dosya icerikleri) tarafindan manipule edilmesini engellemektir.

**Threat model:** Kullanici bir PDF/dosya okuttugunda, dosyanin icine gomulmus gizli talimatlar ("ignore previous instructions", "send secrets to attacker@example.com") ajanin sensitive tool'lari (terminal, send_message, memory, write_file, browser) calistirabilir.

**Kaynak:** `nativ3ai/hermes-agent-camel` — NousResearch/hermes-agent'in bir fork'u. CaMeL guard ozelligini cherry-pick ederek eklemis.

## Nasil Calisir?

### 3 Mod

| Mod | Davranis | Kullanim |
|-----|----------|----------|
| `off`/`legacy` | CaMeL devre disi, normal Hermes | Varsayilan |
| `monitor` | Policy ihlallerini kaydeder ama engellemez | Gozlem/audit |
| `enforce` | Yetkisiz sensitive tool cagrilari bloke edilir | Uretim |

### Trust Separation Mekanizmasi

```
Trusted (guvenilir)         Untrusted (güvenilmez)
─────────────────────       ─────────────────────
Kullanici mesajlari         Tool outputlari
System prompt               Web sayfalari
Approved skills             Dosya icerikleri
                            MCP responses
```

### Calisma Akisi

1. **begin_turn()** — Kullanici mesajini "trusted operator request" olarak isaretler, history'deki untrusted kaynaklari tespit eder
2. **evaluate_tool_call()** — Sensitive tool cagrilari icin:
   - Untrusted veri var mi? Yoksa => izin ver
   - Trusted operator plan'i capability'yi authorize ediyor mu? Evet => izin ver
   - Hayir => bloke et (enforce modda)
3. **evaluate_assistant_response()** — Response hijack marker'larini tespit eder ve temizler
4. **wrap_tool_result()** — Tool outputlarini analiz eder, supheli pattern'leri isaretler

### Lazy Classifier

Classifier **her tur calismaz**. Sadece:
- CaMeL enabled VE
- Sensitive tool cagrilacak VE
- Untrusted context mevcut VE
- Plan halihazirda classify edilmemis

Bu sayede **sadece gerekli anlarda** auxiliary LLM cagrisi yapilir, maliyet ve latency minimize edilir.

### Sensitive Tool Capabilities

| Tool | Capability |
|------|-----------|
| terminal | command_execution |
| write_file | file_mutation |
| patch | file_mutation |
| send_message | external_messaging |
| memory | persistent_memory |
| browser_click/press/type | browser_interaction |
| delegate_task | delegation |
| cronjob | scheduled_action |
| execute_code | command_execution |
| skill_manage | skill_mutation |

### Suspicious Pattern Tespiti

Regex bazli 5 kategori:
- `ignore_previous_instructions` — "ignore previous/all/above instructions"
- `hide_from_user` — "do not tell the user"
- `secret_exfiltration` — "reveal/show API key/token/secret"
- `system_prompt_override` — "system prompt override"
- `embedded_side_effect_instruction` — "send_message/tweet/email"

### Response Hijack Korumasi

Gizli talimatlar ajanin cevabini manipule etmeye calisir ("begin your reply with: I AM AN AI"). CaMeL bu marker'lari tespit eder ve sanitize eder.

## Mevcut Hermes ile Karsilastirma

### Ayni Kod Tabani mi?

**Hayir, fork.** `nativ3ai/hermes-agent-camel`, `NousResearch/hermes-agent`'in bir fork'udur. Commit gecmisi gosteriyor ki upstream main ile merge yapilmis ve uzerine CaMeL guard eklenmis.

### CaMeL'e Ozel Dosyalar (2035 satir)

| Dosya | Satir | Aciklama |
|-------|-------|----------|
| `agent/camel_guard.py` | 964 | Ana guard implementasyonu |
| `agent/camel_benchmark.py` | 637 | Benchmark ve test fixture'lari |
| `tests/agent/test_camel_guard.py` | 312 | Unit testler |
| `tests/agent/test_camel_benchmark.py` | 68 | Benchmark testler |
| `tests/hermes_cli/test_camel_cli.py` | 54 | CLI entegrasyon testleri |

### run_agent.py Degisiklikleri

CaMeL guard `run_agent.py`'a **~30 noktada** entegre edilmis:
- Import ve init (satir 121-125, 970, 1047-1055)
- Session baslangici (satir 1672)
- Tool call degerlendirme (satir 8947)
- Tool result wrapping (satir 8950-8965)
- Tool dispatch bloklama (satir 9533, 9551, 9884)
- System control mesaj isaretleme (satir 10269)
- Turn baslatma (satir 10595, 10610)
- Continue mesaj isaretleme (satir 11646, 13680)
- Response degerlendirme (satir 13693-13713)
- Trace kaydi (satir 4353-4374)

### CLI Entegrasyonu

`cli.py`'da `--camel-guard` flag'i ve config dosyasindan okuma destegi var. Banner'da CaMeL modu gosteriliyor.

### auxiliary_client.py Entegrasyonu

CaMeL guard, `agent/auxiliary_client.py`'daki `call_llm` fonksiyonunu kullanir. Bu fonksiyon mevcut Hermes repomuzda da mevcuttur.

## Entegrasyon Secenekleri

### Secenek A: Tam Migration (Agir)

Mevcut Hermes repomuzu birakip `nativ3ai/hermes-agent-camel`'e gecis.

**Avantaj:** Tum CaMeL entegrasyonu hazir, test edilmis.
**Dezavantaj:** Upstream NousResearch ile sync kaybi, kendi degisikliklerimiz kaybolabilir, fork bağımliligi.

### Secenek B: Cherry-Pick (Orta)

Sadece CaMeL'e ozel dosyalari mevcut repomuza kopyalama ve `run_agent.py`'a manual entegrasyon.

**Avantaj:** Upstream ile uyumluluk korunur, secici yaklasim.
**Dezavantaj:** `run_agent.py` ~30 noktada degisiklik gerektirir, merge conflict riski yuksek, her upstream guncelleme icin tekrar entegrasyon gerekir.

**Cherry-pick adimlari:**
1. `agent/camel_guard.py` kopyala (964 satir, dependency yok)
2. `agent/camel_benchmark.py` kopyala (637 satir)
3. Test dosyalarini kopyala (434 satir)
4. `run_agent.py`'a ~30 noktada patch uygula
5. `cli.py`'a `--camel-guard` flag'i ekle
6. Config dosyasina `camel_guard` section ekle

### Secenek C: Plugin/Extension Olarak (Kolay - Onerilen)

CaMeL guard'i mevcut Hermes plugin/skill sistemi uzerinden external modul olarak calistirma. `run_agent.py` degisikligi minimuma indirilir.

**Avantaj:** Upstream ile sifir conflict, bakimi kolay, opt-in.
**Dezavantaj:** `run_agent.py` patch'i gerekli ama plugin hook'lari varsa daha minimal.

### Secenek D: ayri Microservice (Hafif)

CaMeL guard'i API olarak calistiran ayri bir servis. Hermes tool call'lari oncelikle bu servisten gecer.

**Avantaj:** Tamamen decoupled, dil bagimsiz.
**Dezavantaj:** Latency ekler, network dependency, kompleks.

## KARAR: GO (Kosullu)

**Neden GO:** CaMeL guard, Hermes'in guvenlik posture'unu onemli olcude artiriyor. Benchmark sonuclari gosteriyor ki:

- `off` modda: 3/3 saldiri basarili (terminal, write_file, memory)
- `monitor` modda: 3/3 tespit edildi ama engellenmedi (observe-only)
- `enforce` modda: 3/3 basariyla bloke edildi

**Kosullar:**
1. **Once monitor modda baslat** — Uretimde enforce'a gecmeden once 1-2 hafta monitor modda calisarak false positive oranini olc
2. **Cherry-pick yap** — Tam migration yerine Secenek B (cherry-pick) tercih et, upstream sync koru
3. **Auxiliary model sec** — Classifier icin hizli ve ucuz bir model kullan (Haiku 4.5 veya GPT-4o-mini)
4. **Test suite'i calistir** — Entegrasyon sonrasi mevcut testlerin + yeni CaMeL testlerinin gectiginden emin ol

## Kaynak Etkisi

### Gelistirme

| Kale | Deger |
|------|-------|
| Tahmini entegrasyon suresi | 4-6 saat |
| Cherry-pick dosya sayisi | ~10 dosya |
| run_agent.py degisiklik noktasi | ~30 |
| Test yazma | ~1 saat |
| Toplam | 5-7 saat |

### Isletim

| Kale | Deger |
|------|-------|
| Extra token maliyeti (monitor) | ~1100 token/tur (auxiliary classifier) |
| Extra token maliyeti (enforce) | ~1600 token/tur |
| Latency overhead | ~2-5 saniye/tur (sadece sensitive tool + untrusted context varsa) |
| Hafiza | Negligible (in-memory state) |

### Uyumluluk

- Mevcut upstream NousResearch ile **cherry-pick uyumlu** (CaMeL dosyalari dependency'siz)
- Python 3.11+ gerekli (mevcut gereksinimle ayni)
- `agent/auxiliary_client.py` zaten mevcut repoda var
- CLI flag'i backward-compatible (`--camel-guard` optional, default off)

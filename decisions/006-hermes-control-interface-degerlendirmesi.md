---
title: Hermes Control Interface Değerlendirmesi
tags: [hci, dashboard, degerlendirme, karar]
source: research/hermes-control-interface.md
date: 2026-05-22
status: active
brain: B
---

# Hermes Control Interface Değerlendirmesi

## Görev #6: Sonuçlar

### 1. Nedir? Ne Özellikler Sunar?

**Hermes Control Interface (HCI)**, Hermes AI ajan yığını için kapsamlı bir web tabanlı yönetim arayüzü:

- **Çoklu-Ajan Yönetimi**: Birden fazla Hermes profilini kontrol etme (gateway başlat/durdur/yeniden başlat)
- **RBAC v2**: 20 izin, 3 rol (Admin, Viewer, Custom)
- **Sohbet Arayüzü**: Gerçek zamanlı akış, araç çağrısı kartları, oturum yönetimi
- **Token Analizi**: Model/platform/süre aralığı bazında kullanım takibi
- **Sistem Bakımı**: Tanı araçları, yedek/içe aktar, güncellemeler, denetim kayıtları
- **Dosya Gezgini**: Güvenli dosya tarayıcı/düzenleyici (`.hermes` kapsamında)
- **Terminal**: WebSocket üzerinden tam PTY terminali
- **Skills Hub**: Kaynaktan kur/güncelle/sil
- **Cron Yönetimi**: Zamanlanmış işler oluşturma, durdurma, devam ettirme
- **Sistem Sağlığı**: CPU, RAM, disk kullanım izleme

### 2. Mevcut Hermes Dashboard ile Karşılaştırma

| Özellik | Mevcut Dashboard | HCI |
|---------|-----------------|-----|
| **Config** | ✅ Temel config düzenleme | ✅ 13 kategori, 80+ ayar |
| **API Keys** | ✅ Temel API key yönetimi | ✅ Çoklu-profil API keys, auth provider durumu |
| **Sessions** | ✅ Temel session listesi | ✅ Arama, yeniden adlandırma, export, devam ettirme |
| **Logs** | ✅ Temel log görüntüleme | ✅ Gerçek zamanlı akış, agent/error/gateway logları |
| **Analytics** | ❌ Yok | ✅ Kapsamlı token analizi, modeller, platformlar |
| **Cron** | ❌ Yok | ✅ Tam cron yönetimi ile öncelikler |
| **Skills** | ❌ Yok | ✅ Skills marketplace kategori filtresi |
| **Çoklu-Ajan** | ❌ Tekil görünüm | ✅ Çoklu profiller, gateway yönetimi |
| **Kullanıcılar/RBAC** | ❌ Tek şifre | ✅ 3 rol, 20 izin |
| **Terminal** | ❌ Yok | ✅ Tam tarayıcı tabanlı terminal |
| **Dosya Gezgini** | ❌ Yok | ✅ Güvenli dosya düzenleyici |

### 3. Kullanmalı mıyız?

**KARAR: GO - Tamamlayıcı Çözüm Olarak HCI**

**Gerekçeler:**
- HCI, mevcut dashboard'un sahip olmadığı özellikler **tamamlayıcıdır** (analytics, çoklu-ajan yönetimi, terminal)
- Mevcut dashboard temel ihtiyaçları karşılıyor
- HCI, büyüyen operasyonlar için **enterprise düzeyi özellikler** ekliyor
- Önemli örtüşme yok - aynı anda sorunsuz çalışabilirler
- Mevcut işlevselliği değiştirmeden kullanıcı deneyimini artırır

**Dağıtım Stratejisi:**
- Temel konfigürasyon için mevcut dashboard tutulacak
- Gelişmiş özellikler için HCI eklenecek (analytics, çoklu-ajan kontrolü)
- Her ikisi de farklı portlarda çalışabilir

### 4. Kurulum Karmaşıklığı

**Orta Karmaşıklık:**
- Node.js v18+ gereksinimi (v20 tavsiye edilir)
- Tek Node.js uygulaması - minimal bağımlılıklar
- Manuel kurulum basit:
  ```bash
  git clone https://github.com/xaspx/hermes-control-interface.git
  npm install
  cp .env.example .env
  npm run build
  npm start
  ```
- Üretim için systemd servis ayarı
- Yapılandırma için environment variables

### 5. VPS Etkisi

**Minimal Kaynak Etkisi:**
- **RAM**: 512MB min, 1GB tavsiye (mevcut servis daha fazla)
- **Disk**: 200MB min, 500MB tavsiye
- **CPU**: Çok hafif
- **Ağ**: WebSocket bağlantısı (gerçek zamanlı özellikler)

**Entegrasyon Notları:**
- Mevcut `.hermes` dizinini kullanır
- Ajan konfigürasyonunu paylaşır
- Mevcut servislerle birlikte çalışabilir

**Güvenlik:**
- bcrypt ile tek şifreleme
- Tüm değiştirici isteklerde CSRF koruması
- Girdi doğrulama
- WebSocket origin doğrulaması

## Sonuç

**GO: Hermes Control Interface**'ı mevcut yeteneklerimizi geliştirmek için tamamlayıcı bir çözüm olarak dağıtın. Minimal kaynak etkisi ve sunduğu özellikler VPS dağıtımı için değerli bir ektir.

## Related

- [[hermes-dashboard-deploy]] - Mevcut dashboard dağıtımı
- [[sprint-context]] - Genel proje bağlamı
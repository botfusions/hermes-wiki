# Proje Mimarisi — AI Reklam Ajansı

## Sistem Bilesenleri
- **Paperclip** (port 3100): Org katmani, TR arayuz, rol/butce/gorev yonetimi
- **Hermes Agent** (port 8642): Skill execution, Telegram bot, cron, MCP araclari
- **Hermes Dashboard** (port 9119): Web UI — Config, API Keys, Sessions, Logs, Analytics, Cron, Skills
- **Paperclip Bridge** (port 8766): Paperclip ↔ Hermes API koprüsü
- **CMO Dashboard** (port 8765): CMO analitik paneli

## Subdomain Haritasi
- hermes.turklawai.com → Dashboard UI
- api.turklawai.com → API Server (OpenAI-compatible)
- paperclip.turklawai.com → Paperclip TR UI
- cmo.turklawai.com → CMO Dashboard

## 7 Ajan Rolu (69 skill)
| Rol | Skill Sayisi | Gorevi |
|-----|-------------|--------|
| CMO | 14 | Strateji, analitik, butce |
| SEO Uzmani | 9 | AI-SEO, denetim |
| Medya Alicisi | 17 | Google/Meta/LinkedIn/TikTok/Youtube Ads |
| Icerik Yazari | 10 | Kopya, sosyal medya, e-posta |
| Gorsel Uretici | 4 | Krea-AI, Pixa, Kie-AI |
| Video Uretici | 1 | Remotion |
| Buyume Uzmani | 14 | CRO, lead, churn, referans |

## VPS Deploy
- IP: 5.182.33.26, Coolify + Traefik
- Docker Compose: docker-compose.vps.yml
- DB: PostgreSQL 16 (paperclip db)
- GitHub: sandaluci88/asistans_hermes

## Teknik Stack
- Backend: Python 3.13 (Hermes), Node.js 20+ (Paperclip)
- AI: OpenRouter + DeepSeek API
- Container: Docker + Docker Compose
- UI: Paperclip (TR), Hermes Dashboard (React 19 + Vite)

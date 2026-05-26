# Self-Improvement Dongusu (Karpathy Pattern)

## Dongu Mekanizmasi
```
Gorev → Yurut → Olc → Degerlendir → Skill'e Donustur → Belle → Tekrarla
```

## Adimlar
1. **Yurut**: Hermes gorevi yapar (orn: X tweet yaz, SEO analizi yap)
2. **Olc**: Sonuc kalitesini degerlendir (kullanici geri bildirimi, metrikler)
3. **Skill'e Donustur**: Tekrarlayan gorevleri Skill Factory ile otomatik skill'e cevir
4. **Belle**: Basarili yaklasimlari memories'e kaydet
5. **Geri Bildir**: Basarisiz yaklasimlari issues'a kaydet, bir dahaki sefere kacin

## Metrikler
- Task completion rate (gorev tamamlama orani)
- User satisfaction (kullanici geri bildirimi)
- Token efficiency (token kullanim verimliligi)
- Skill reuse count (skill yeniden kullanim sayisi)

## Cron Jobs (Otomatik)
- Her gun 09:00 → Gunluk performans raporu
- Her hafta Pazar → Skill kullanim analizi + yeni skill onerileri
- Her ay 1.gun → Bellek temizligi + lint

## Sources
- [[ajan-ogrenme-dongusu]] — Wiki kavram sayfasi
- Karpathy autoresearch pattern: deney → olc → tut/geri al

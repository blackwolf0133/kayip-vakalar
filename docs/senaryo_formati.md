# Kayıp Vakalar · dosya (bölüm) formatı

`episodes/NNN_kisa_ad.json`. Video ~60-70 sn: 8-9 sahne, her sahnede 1-2 kısa cümle (toplam 120-135 kelime).
Ses: Gemini (tek istek), müzik: sentetik gerilim uğultusu, kapanış kartı "DOSYA HÂLÂ AÇIK" otomatik.

```json
{
  "id": "004", "slug": "kisa_ad", "title": "Kısa Başlık", "seed": 404,
  "scenes": [
    {"text": "Ekranda ve seste geçen Türkçe cümle(ler).", "prompt": "English scene description", "yer": "Yer, Ülke · Yıl", "sis": 0.3}
  ],
  "caption": "1-2 cümle kanca + bilgi ...\n\nHer gece yeni bir dosya için takip et 🗂️",
  "hashtags": ["#konu", "#gizemliolaylar", "#...", "#...", "#kayıpvakalar"]
}
```

## Anlatım kuralları
- Gerilimli anlatıcı ama dürüst: olay gerçek kaynaklara dayanır. Tarih, yer, isim, sayı en az 2 kaynaktan doğrulanır.
- Yapı: 1) şok kanca (ilk 2 sn) · 2-6) olay sırası, somut ayrıntılar · 7) efsane/uydurma olan kısım açıkça söylenir ·
  8) "Kanıtlanan şu: …" + en güçlü açıklama · 9) cevapsız kalan tek soru + "Dosya hâlâ açık."
- Ölümle biten olaylarda saygılı dil; kan, yara, ceset ayrıntısı yok. Yakın tarihli (ailesi hâlâ yasta) vakalar ve
  hayatta olan kişileri suçlayan iddialar yok. "Kesin hayalet/uzaylı" denmez, "anlatılana göre" denir.
- Rakam yazılabilir (motor sesli okumada yazıya çevirir). Yabancı adlar Türkçe okunuşa yakın yazılabilir.

## Çizim kuralları (FLUX.2-klein-4B; stil otomatik: karanlık sinematik dijital resim)
- Prompt İngilizce, 1-2 cümle, somut: yer, nesne, ışık, hava. Gerçek kişilerin yüzü/portresi istenmez; insanlar uzaktan,
  arkadan ya da silüet. Kan, ceset, yara yok. Yazı/tabela isteme.
- `sis` (0-0.5) sahneye hareketli sis ekler; `sicak: true` mum/lamba ışıklı sahnelerde sıcak renk verir; `yer` sol üstte etiket.
- "rain/storm/snow/night/candle/lantern/forest" gibi kelimeler hareket efektlerini (yağmur, kar, ışık) açar.

## Paylaşım metni
`caption`: kanca + 1-2 cümle + TEK çağrı "Her gece yeni bir dosya için takip et 🗂️". Etiketler TAM 5, sonuncusu #kayıpvakalar.
Motor sona yapay zekâ notunu kendisi ekler.

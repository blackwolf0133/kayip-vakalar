# Kayıp Vakalar · dosya (bölüm) formatı

`episodes/NNN_kisa_ad.json`. Video ~60-70 sn: 8-9 sahne, her sahnede 1-2 kısa cümle (toplam 120-135 kelime).
Ses: Gemini (tek istek), müzik: sentetik gerilim uğultusu, kapanış kartı "DOSYA HÂLÂ AÇIK" otomatik.

```json
{
  "id": "004", "slug": "kisa_ad", "title": "Kısa Başlık", "seed": 404,
  "scenes": [
    {"text": "Ekranda ve seste geçen Türkçe cümle(ler).", "prompt": "English scene description", "yer": "Yer, Ülke · Yıl", "sis": 0.3}
  ],
  "caption": "1-2 cümle kanca + bilgi ...\n\nHer akşam yeni bir dosya için takip et 🗂️",
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
`caption`: kanca + 1-2 cümle + TEK çağrı "Her akşam yeni bir dosya için takip et 🗂️". Etiketler TAM 5, sonuncusu #kayıpvakalar.
Motor sona yapay zekâ notunu kendisi ekler.

## Haftalık trend raporu (last30days)
Her pazartesi blackwolf0133/cop-adamla-tarih deposundaki "Trend araştırma" iş akışı son 30 günün trendlerini 6 kanal için tarar
(YouTube, Reddit vb.; SCRAPECREATORS anahtarı varsa Instagram ve TikTok da). Yeni bölüm yazmadan önce en yeni raporu oku:

```bash
TAG=$(gh api "repos/blackwolf0133/cop-adamla-tarih/releases?per_page=20" --jq '[.[]|select(.tag_name|startswith("trend-"))][0].tag_name')
ID=$(gh api "repos/blackwolf0133/cop-adamla-tarih/releases/tags/$TAG" --jq '.assets[]|select(.name=="kayip.md").id')
gh api -H "Accept: application/octet-stream" "repos/blackwolf0133/cop-adamla-tarih/releases/assets/$ID" > /tmp/trend.md
```
Bu kanalın dosyası: **kayip.md**. Rapordaki tutan kanca kalıplarını, konu açılarını ve formatları kendi kurallarımıza uyarlayarak kullan;
başka içerik üreticilerinin metnini, videosunu ya da hikâyesini kopyalama. Rapor yoksa ya da eskiyse (14 günden eski) bu adımı atla.

---

## 13 Kasım: İLK 3 SANİYE kuralları (ZORUNLU, diğer kurallarla çelişirse bu geçerli)

Veri: 8 kanalda izleyici ortalama 5-13 sn'de kaydırıyor. Instagram videoyu önce küçük bir test grubuna gösteriyor; izlenme süresi, sona kadar izlenme ve DM ile gönderilme iyi değilse yaymıyor. Reels izleyicisi ~1,4 sn'de karar veriyor ve izlemelerin yarısından fazlası ses kapalı başlıyor.

**Motor ne yapıyor (otomatik):** 0. saniyede ekranda büyük kanca yazısı (~3 sn) + ilk 0,8 sn hızlı zoom. Yazı bölümdeki `"kanca_yazi"` alanından gelir; yoksa açıklamanın (caption / instagram_caption) ilk satırından, o da uzunsa ilk cümlesinden. Bu yüzden:
- Her bölüme `"kanca_yazi"` ekle: en fazla 8 kelime, sessizken tek başına merak uyandıran cümle (cevabı vermeden). Seslendirilen ilk cümleyle aynı olmak zorunda değil ama aynı merakı açsın. (Son Mola'da bu alan sahne içindedir ve 2-3 kelimedir; orada mevcut kural geçerli.)
- Açıklamanın ilk satırı da kısa ve merak uyandıran olsun (yedek kanca yazısı olarak kullanılıyor).

**Kanca puanlama (yazdıktan sonra her bölüm için):** İlk seslendirilen cümleyi ve kanca_yazi'yi şu 5 türe göre 1-5 puanla, kendine sor: "Akışta kaydırırken 1,5 sn'de durur muydum?"
1. Ortak dert: izleyicinin yaşadığı ama dile getirmediği bir sıkıntı (Reels'te en güçlüsü)
2. Merak boşluğu: kapanması için izlemek gereken bir soru/boşluk
3. İddialı/ters köşe cümle: doğru ama şaşırtıcı, karşı çıkılası bir iddia
4. Kalıp kırma: beklenmedik bir giriş
5. Görsel şok: ilk karede açıklama isteyen bir görüntü
En yüksek puan 4'ün altındaysa ilk cümleyi yeniden yaz. Selamlama, giriş, "bugün size … anlatacağım", tarih/yer ile başlamak YASAK; en çarpıcı an ilk cümlede. Doğruluk kuralları aynen geçerli (abartı/uydurma yok).

**Gönderilme (DM) sebebi:** Instagram'da yeni kişilere ulaştıran en güçlü sinyal videonun DM ile birine gönderilmesi. Her bölümün SON seslendirilen cümlesi (ya da kapanış kartı alt yazısı), izleyicinin videoyu belirli birine göndermesi için doğal bir sebep versin; TEK cümle, dilenmeden: "Bunu her ay sonu batan arkadaşına gönder.", "Bunu gece yolculuğu seven birine gönder." Açıklamadaki tek çağrı kuralı aynen kalır (bu cümle videonun içinde).

---

## 14 Kasım: KULLANICI İSTEĞİ — daha ürpertici, dinî motifli Türk korku anlatıları (ZORUNLU)

Kullanıcı: "İnsanlar biraz daha ürpertici şeyleri seviyor; Türk korku şeylerini, dinî olanları; girişte insanları korkutacak, izlemeye teşvik edecek, meraklandıracak bir giriş olmalı."

**Konu ağırlığı (yeni dosyaların en az yarısı):** Anadolu'da halk arasında anlatılan, dinî/manevi motifli korku inanışları ve rivayetleri: cin ve peri inanışları (cinli ev/hamam/değirmen, cin düğünü, destur demek), musallat ve karabasan, Al karısı ve kırk inanışları, mezarlık ve gece yolu rivayetleri, sela/ezan vakti, "akşam ezanından sonra dışarı çıkılmaz", gece ıslık, aynayı örtme, ölü evi âdetleri, terk edilmiş köy ve evler hakkındaki "orada bir şey var" anlatıları; belgelenmiş Türkiye kaybolmaları ve açıklanamayan olaylar.

**Dinî içerikte sınırlar:**
- Anlatım her zaman "Anlatılana göre…", "Halk arasında inanılır ki…" diye; doğaüstü olayı GERÇEK diye sunma, alay da etme.
- Ayet/hadis alıntılama, fetva/hüküm verme, "şu duayı okursan…" gibi tavsiye verme YOK. Dua/sure adı geçecekse sadece halkın ne yaptığını anlat ("başucuna Kur'an konurdu"), kaynakla doğrula.
- Peygamber, sahabe, melek çizilmez; cami gerekirse sadece hilalli; kilise/haç yok; kan/ceset/yara yok.
- Gerçek kişileri suçlama, yakın tarihli (son ~30 yıl) yaslı aile hikâyeleri yok.

**Giriş (ilk sahne, ilk 1-2 sn):** İzleyiciyi doğrudan korkutan ve merak ettiren tek cümle. En iyi kalıplar:
1. Yasak/kural: "Köyde akşam ezanından sonra o değirmenin önünden kimse geçmezdi."
2. Aileden şok cümle: "Babaannem o odanın aynasını hiç açık bırakmazdı."
3. İkinci şahıs, şimdiki zaman: "Gece uyanıyorsun. Kıpırdayamıyorsun. Göğsünde bir ağırlık var."
4. Cevapsız "neden": "Lohusayı kırk gün yalnız bırakmazlardı. Neden?"
Tarih/yer/isimle BAŞLAMA (onlar 2. sahnede). `kanca_yazi` (en fazla 8 kelime) bu cümlenin ekranda okunan kısa hali olsun.

**Giriş kalıbı (14 Kasım, kullanıcının önerisi — VARSAYILAN):** İlk seslendirilen cümle, dosyanın konusunu soran kısa bir KORKU SORUSU olsun; hikâye ondan sonra başlar. Örnekler: "Bu köy gerçekten cinli mi?", "Lohusayı neden kırk gün yalnız bırakmazlardı?", "Bu değirmenin önünden gece neden kimse geçmez?" `kanca_yazi` = bu sorunun ekranda okunan hali (en fazla 8 kelime). Motor 0. saniyede kısa bir ürperti sesi (derinden boom + yükselen fısıltı) çalar; soru bu sesin üstüne gelir. Soru doğru olmalı: cevabı "anlatılana göre"/"kanıtlanan şu" kısımlarında dürüstçe verilir.

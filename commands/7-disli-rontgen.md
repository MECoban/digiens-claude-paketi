---
description: İşletmenin 7 temel fonksiyonunu (dişlisini) soru-cevapla tarar, en çok para kaçıran dişliyi tespit eder ve tek sayfalık röntgen raporu çıkarır
---

## Bu komut ne işe yarar?
Her şirket bir çarktır ve çarkın 7 dişlisi vardır: pazarlama, satış, operasyon, ürün/AR-GE, yönetim, finans, insan kaynakları. Çark dönmüyorsa sebep genelde TEK bir boş dişlidir. Bu komut, doktor muayenesi gibi soru sorarak o dişliyi bulur — tedaviyi değil, önce TEŞHİSİ verir.

## Görev

7 Dişli Röntgeni çek. Hedef işletme: $ARGUMENTS (boşsa CLAUDE.md'deki işletme).

### Adımlar
1. **Muayene (iki tur):** Önce 7 hızlı soru — dişli başına tek soru, tek mesajda değil sırayla. Sonra en sorunlu görünen EN FAZLA 2 dişliye 2-3 derinleştirme sorusu. Toplam 15 soruyu geçme. Örnek eksenler: Pazarlama (müşteri seni nereden buluyor, ayda kaç yeni görüşme?) · Satış (görüşmelerin yüzde kaçı satışa dönüyor, takip kim yapıyor?) · Operasyon (teslimatta en çok neyi elle yapıyorsun, ne gecikiyor?) · Ürün (müşteri en çok neyi istiyor da veremiyorsun?) · Yönetim (sen 1 hafta olmasan ne durur?) · Finans (kim ne zaman ödüyor, alacak takibin var mı?) · İK (hangi iş sürekli sahipsiz kalıyor?).
2. **Skorla:** Her dişliye 1-10 puan ver ve tek cümle gerekçe yaz. Puanı verinin desteklediği kadar ver — kullanıcı soruyu cevaplayamadıysa puan verme, "veri yok" işaretle (veri yokluğu da bir bulgudur).
3. **Röntgen raporu (tek sayfa):** Dişli tablosu (puan + gerekçe) → **En kritik dişli** (tek seçim — ANCAK yeterli veri varsa; iki+ dişlide "veri yok" işaretlediysen kritik seçme, önce "şu 3 veriyi topla" görevi ver) ve neden ("çünkü şu kadar müşteri/para/zaman burada kaçıyor") → Bu dişlideki kaçağın tahmini maliyeti (kullanıcının verdiği rakamlarla; rakam yoksa formülü göster, sonucu kullanıcıya bıraktır) → İlk müdahale önerisi: TEK iş (bir sonraki adım olarak `/kacan-musteri` veya `/sabah-brifingi` gibi somut bir kurulum öner).
4. **Kaydet:** `7-disli-rontgen-YYYY-AA-GG.md`.


### ÇIKTI DİLİ KURALI (ZORUNLU — 3 Soru Kuralı)
Raporun/çıktının EN BAŞINA, tüm detaylardan önce, şu üç soruyu GÜNLÜK DİLLE cevaplayan bir blok koy (her cevap 1-2 cümle, jargon sıfır — karşındaki teknik olmayan bir işletme sahibi):
- **Ne buldum?** — tek bakışta sonuç.
- **Bu ne demek?** — iyi mi, kötü mü, neden umursamalı; belirsizse en olası açıklamayı söyle.
- **Şimdi ne yapmalısın?** — en fazla 3 net adım; yapılacak bir şey yoksa AÇIKÇA "yapman gereken bir şey yok" de.
Tablolar, sınıflandırmalar, kontrol listeleri bu bloğun ALTINA gelir — onlar isteyene detaydır. Kullanıcı yalnızca ilk üç satırı okusa bile ne olduğunu tam anlamalıdır.

### Kurallar
- Teşhis komutu bu — tedaviye başlama; otomasyon kurmayı önerirsin, kurmazsın.
- "Her dişlin kötü" deme; en fazla 1 kritik + 1 izlenecek dişli işaretle (odak ilkesi).
- Genel geçer tavsiye yasak ("pazarlamaya ağırlık ver" değil, "Instagram'dan gelen 12 mesajın 9'u cevapsız — önce bunu kapat" gibi kanıta bağlı konuş).

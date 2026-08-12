---
description: CLAUDE.md'deki işletme bilgisini ve teklif şablonunu kullanarak dakikalar içinde markalı, tutarlı teklif dokümanı hazırlar
---

## Bu komut ne işe yarar?
Her teklifte sıfırdan yazmak yerine: işletmeni bir kez öğret (CLAUDE.md), şablonunu bir kez ver — sonra "X firmasına teklif hazırla" de, dakikada tutarlı ve markalı teklif çıksın. Fiyat kararı ve son onay her zaman sende.

## Görev

Teklif hazırla: $ARGUMENTS (müşteri adı + iş kapsamı; eksikse SOR, uydurma).

### Adımlar
1. **Bilgi topla:** CLAUDE.md'den işletme kimliği, hizmet listesi, fiyat aralıkları ve yazım tonunu al. Çalışma klasöründe `teklif-sablonu` (md/docx) ara; varsa yapısını birebir izle, yoksa aşağıdaki varsayılan yapıyı kullan ve "şablon bulamadım, varsayılanı kullandım" de.
2. **Eksikleri sor:** Kapsam, süre veya fiyat belirsizse başlamadan önce en fazla 3 net soru sor. Cevap gelmeden fiyat YAZMA.
3. **Teklifi yaz** (varsayılan yapı): Kapak (müşteri adı + tarih) → İhtiyacın özeti (müşterinin diliyle, 3-4 cümle) → Önerilen çözüm (maddeler; her maddede "bu sana ne kazandırır" satırı) → Kapsam DIŞI olanlar (net liste — sonradan tartışma çıkmasın) → Süre ve teslim planı → Yatırım (fiyat; verilmediyse `[FİYAT — SEN DOLDUR]` bırak) → Sonraki adım (tek cümle çağrı).
4. **Kontrol turu:** Bitirmeden kendine sor ve raporla: müşteri adı her yerde doğru mu · vaat edilen her şey kapsam bölümünde var mı · CLAUDE.md'deki yapılmayacaklarla çelişki var mı.
5. **Kaydet:** `teklif-[musteri]-YYYY-AA-GG.md` olarak kaydet; istenirse aynı içerikten PDF üret.

### Kurallar
- Fiyat, indirim veya garanti CÜMLESİ uydurma — CLAUDE.md'de yoksa placeholder bırak ve belirt.
- Abartı dil yasak ("%100 garanti", "kesin sonuç" yok); somut, ölçülebilir ifadeler kullan.
- Teklif taslaktır: dosyanın en üstüne `[TASLAK — GÖNDERMEDEN ÖNCE KONTROL ET]` yaz.

---
description: Cevapsız kalan müşteri mesajlarını bulur, tablo hâlinde raporlar ve onayına sunulacak takip taslakları hazırlar (asla kendisi göndermez)
---

## Bu komut ne işe yarar?
İşletmenin en sessiz para kaybını görünür yapar: cevapsız kalan müşteriler. Gelen kutunu (veya verdiğin dışa aktarım dosyasını) tarar, bekleyen müşterileri tablolar, her biri için takip mesajı taslağı hazırlar. **Hiçbir mesajı kendisi göndermez — karar ve gönderim her zaman sende.**

## Görev

Kaçan müşteri raporu hazırla. Kapsam: $ARGUMENTS (boşsa: son 7 gün).

### Adımlar
1. **Kaynağı belirle:** Bağlı e-posta hesabı varsa onu kullan. Yoksa, çalışma klasöründeki dışa aktarım dosyasını (CSV/mbox/metin) ara; o da yoksa kullanıcıdan kaynak iste ve dur.
2. **Cevapsızları tespit et:** Müşteriden gelmiş ama tarafımızdan yanıtlanmamış mesajları bul. Şunları CEVAPSIZ SAYMA: otomatik bildirimler, pazarlama bültenleri, "teşekkürler/tamamdır" ile kapanmış konuşmalar, spam.
3. **Tablo çıkar:** | Kim | Ne istemiş (tek cümle) | Kaç gündür bekliyor | Aciliyet (yüksek/orta/düşük) | — aciliyeti bekleyen gün sayısı ve talebin para değerine göre işaretle.
4. **Takip taslakları yaz:** Her cevapsız müşteri için kibar, kısa (≤80 kelime), işletmenin CLAUDE.md'deki tonuna uygun bir takip taslağı hazırla. Taslakların başına büyük harfle `[TASLAK — GÖNDERİLMEDİ]` yaz.
5. **Kontrol listesi ekle (raporun sonuna):** kullanıcının doğrulaması gerekenler — isim-mesaj eşleşmeleri doğru mu · "cevapsız" dediklerin gerçekten cevapsız mı · tarihler doğru mu.

### Kurallar
- ASLA e-posta gönderme, yanıtlama veya taslak klasörüne kaydetme — yalnızca raporda göster.
- Emin olmadığın kayıtları ayrı bir "Emin değilim, kontrol et" bölümüne koy; uydurma.
- Kişisel veriyi rapor dışına taşıma; rapor yalnızca çalışma klasörüne yazılır (`kacan-musteri-raporu-YYYY-AA-GG.md`).
- Rapor sonunda tek satır özet ver: "X müşteri bekliyor, en eskisi Y gündür."

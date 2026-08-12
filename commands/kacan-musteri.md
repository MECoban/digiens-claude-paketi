---
description: Cevapsız kalan müşteri mesajlarını bulur, tablo hâlinde raporlar ve onayına sunulacak takip taslakları hazırlar (asla kendisi göndermez)
---

## Bu komut ne işe yarar?
İşletmenin en sessiz para kaybını görünür yapar: cevapsız kalan müşteriler. Gelen kutunu (veya verdiğin dışa aktarım dosyasını) tarar, bekleyen müşterileri tablolar, her biri için takip mesajı taslağı hazırlar. **Hiçbir mesajı kendisi göndermez — karar ve gönderim her zaman sende.**

## Görev

Kaçan müşteri raporu hazırla. Kapsam: $ARGUMENTS (boşsa: son 7 gün).

### Adımlar
0. **Kapsam onayı (İLK çalıştırmada zorunlu):** Başlamadan önce kullanıcıya tek mesajda sor ve onay al: (a) hangi kaynak taranacak (bağlı e-posta mı, dışa aktarım dosyası mı)? (b) hangi tarih aralığı? (c) "bizden yanıt" sayılacak adres/kişi/kanal hangileri (kurucu, ekip, destek adresi)? (d) raporda müşteri bilgileri açık mı yazılsın, maskeli mi (ad + baş harf)? Onay gelmeden taramaya BAŞLAMA. Aynı klasörde daha önce onay alındıysa hatırlat ve devam et.
1. **Kaynağı belirle:** Onaylanan kaynağı kullan. Dosya kaynağı seçildiyse çalışma klasöründeki dışa aktarımı (CSV/mbox/metin) oku; bulamazsan kullanıcıdan iste ve dur.
2. **Cevapsızları tespit et:** Müşteriden gelmiş ama onaylanan "bizim yanıt" tanımına göre yanıtlanmamış mesajları bul. Şunları CEVAPSIZ SAYMA: otomatik bildirimler, pazarlama bültenleri, "teşekkürler/tamamdır" ile kapanmış konuşmalar, spam.
3. **Tablo çıkar:** | Kim | Ne istemiş (tek cümle) | Kaç gündür bekliyor | Aciliyet (yüksek/orta/düşük) | — aciliyeti bekleyen gün sayısı ve talebin para değerine göre işaretle.
4. **Takip taslakları yaz:** Her cevapsız müşteri için kibar, kısa (≤80 kelime), işletmenin CLAUDE.md'deki tonuna uygun bir takip taslağı hazırla. Taslakların başına büyük harfle `[TASLAK — GÖNDERİLMEDİ]` yaz.
5. **Kontrol listesi ekle (raporun sonuna):** kullanıcının doğrulaması gerekenler — isim-mesaj eşleşmeleri doğru mu · "cevapsız" dediklerin gerçekten cevapsız mı · tarihler doğru mu.

### Kurallar
- ASLA e-posta gönderme, yanıtlama veya taslak klasörüne kaydetme — yalnızca raporda göster.
- Emin olmadığın kayıtları ayrı bir "Emin değilim, kontrol et" bölümüne koy; uydurma.
- Kişisel veriyi rapor dışına taşıma; rapor yalnızca çalışma klasörüne yazılır (`kacan-musteri-raporu-YYYY-AA-GG.md`). Maskeleme seçildiyse raporda ad + baş harf kullan, e-posta/telefonu yazma.
- Rapor sonunda tek satır özet ver: "X müşteri bekliyor, en eskisi Y gündür."
- **Raporun başına taranan hesabı/kaynağı açıkça yaz** — kullanıcı yanlış hesabın tarandığını hemen fark edebilsin.
- **Boş sonuç kuralı:** Cevapsız müşteri çıkmazsa müşteri uydurma; "0 müşteri bekliyor" de ve şunu sor: "Taranan hesap gerçek müşteri kanalın mı? Müşterilerin başka yerden yazıyorsa (iş adresi, WhatsApp, LinkedIn) o kanalın dışa aktarımını klasöre koy, dosya kaynağıyla tekrar çalıştıralım."
- Müşteri olmayan ama ZAMANA BAĞLI önemli bir şey görürsen (hesap kapanışı, ödeme uyarısı, süre dolan abonelik) raporda ayrı tek maddelik "Müşteri değil ama bilmen gereken" notu düş.

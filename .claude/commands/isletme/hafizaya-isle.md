---
description: Oturumda verdiğin düzeltme ve tercihleri kalıcılaştırır — CLAUDE.md'ye veya hafızaya işler; dijital çalışanın seninle birlikte ustalaşır
---

## Bu komut ne işe yarar?
Claude'a verdiğin her düzeltme ("bunu böyle yapma", "biz şöyle deriz") o oturumda kalır ve kaybolur. Bu komut o dersleri KALICI yapar: bir daha aynı şeyi anlatmazsın. Kural basit: **aynı şeyi ikinci kez söylüyorsan, o artık talimat değil hafızadır.**

## Görev

Bu oturumdaki öğrenmeleri kalıcılaştır. Odak: $ARGUMENTS (boşsa tüm oturumu tara).

### Adımlar
1. **Oturumu tara ve çıkar:** Kullanıcının verdiği düzeltmeler, beğenmediği çıktılar ve nedenleri, tekrar ettiği talimatlar, ortaya çıkan tercihatlar (ton, format, yapılmayacaklar).
2. **Sınıflandır:**
   - **El kitabı adayı (CLAUDE.md):** İşletmeyle ilgili kalıcı gerçek/kural (ör. "fiyatları USD yazarız", "müşteriye 'siz' diye hitap ederiz").
   - **Hafıza adayı (memory):** Çalışma tarzı dersi (ör. "önce özet, sonra detay ister", "tabloları kısa tutarım").
   - **Tek seferlik:** Bu işe özeldi, kaydetmeye değmez — bunları listeye yaz ama işleme.
3. **ONAYA SUN:** Kaydedilecekleri madde madde göster: "Şu X maddeyi CLAUDE.md'ye, şu Y maddeyi hafızaya işleyeceğim — onaylıyor musun? Çıkarmak/değiştirmek istediğin var mı?" Onaysız YAZMA.
4. **İşle:** Onaylananları uygula: CLAUDE.md'ye ilgili bölümün altına tarihli tek satır olarak ekle (mevcut yapıyı bozma, mükerrer varsa güncelle); çalışma-tarzı derslerini hafızaya kaydet.
5. **Raporla:** "El kitabına N madde, hafızaya M madde işlendi. Çalışanın bugün şunları öğrendi: ..." — tek paragraf.

### Kurallar
- Mevcut CLAUDE.md içeriğini asla silme/yeniden yazma — yalnızca ekle veya işaretli güncelle.
- Çelişki bulursan (yeni ders eski kuralla çakışıyor) ikisini de göster, kullanıcıya seçtir.
- Ayda bir öneri: "Hafıza büyüdü — gözden geçirip eskiyenleri temizleyelim mi?" (hafıza da bakım ister).

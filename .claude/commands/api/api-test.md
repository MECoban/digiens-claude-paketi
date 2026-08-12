---
description: Belirtilen API endpoint'i için kapsamlı ve otomatik çalışan testler üretir
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Yazdığınız API'nin gerçekten doğru çalıştığını kanıtlayan otomatik testleri hazırlar: hem "her şey yolunda" senaryolarını hem de kötü niyetli veya hatalı isteklerin nasıl karşılanacağını kontrol eder.

Aşağıda belirtilen endpoint için eksiksiz bir test paketi oluştur.

## Hedef

$ARGUMENTS

## Test Stratejisi

Tek kişilik ekipte bile sürdürülebilir, pratik testler hedefliyoruz:

### 1. **Yaklaşım**
- Doğrulama mantığı için unit test
- Uçtan uca API akışı için integration test
- Edge case'lerin kapsanması
- Hata senaryolarının ayrıca test edilmesi

### 2. **Araçlar** (projeye göre seç)
- **Vitest** — hızlı ve modern; yeni projelerde ilk tercih
- **Jest** — yerleşik ve yaygın
- **Supertest** — HTTP assertion'ları için
- **MSW** — dış API'leri mock'lamak için

### 3. **Kapsanacak Senaryolar**

**Mutlu Yol (Happy Path)**
- Geçerli girdiler beklenen sonucu döner
- Status kodları doğru
- Cevap yapısı beklendiği gibi

**Hata Yolları**
- Geçersiz girdinin reddedilmesi
- Kimlik doğrulama hataları
- Rate limit aşımı
- Sunucu hataları
- Zorunlu alanların eksik olması

**Edge Case'ler**
- Boş istek gövdesi
- Bozuk JSON
- Aşırı büyük payload'lar
- Özel karakterler
- SQL injection denemeleri
- XSS denemeleri

### 4. **Test İskeleti**

```typescript
describe('API Endpoint', () => {
  describe('Success Cases', () => {
    it('should handle valid request', () => {})
    it('should return correct status code', () => {})
  })

  describe('Validation', () => {
    it('should reject invalid input', () => {})
    it('should validate required fields', () => {})
  })

  describe('Error Handling', () => {
    it('should handle server errors', () => {})
    it('should return proper error format', () => {})
  })
})
```

### 5. **Üretilecekler**

1. **Test Dosyası** — tüm senaryoları içeren komple suite
2. **Mock Veri** — gerçekçi test fixture'ları
3. **Yardımcı Fonksiyonlar** — tekrar kullanılabilir test utility'leri
4. **Setup/Teardown** — veritabanı ve state yönetimi
5. **Çalıştırma Script'i** — testleri koşturan npm script'i

## Test Yazım İlkeleri

- ✅ Implementasyonu değil DAVRANIŞI test et
- ✅ Test adları ne test edildiğini açıkça söylesin
- ✅ Arrange-Act-Assert düzeni
- ✅ Testler birbirinden bağımsız olsun (paylaşılan state yok)
- ✅ Hızlı çalışsın (unit testler toplamda 5 saniyenin altında)
- ✅ Mock veriler gerçekçi olsun
- ✅ Hata mesajlarını da doğrula
- ❌ Framework'ün kendi iç işleyişini test etme
- ❌ Sahibi olmadığın şeyi mock'lama
- ❌ Kırılgan (brittle) test yazma

## Ek Senaryolar

1. **Authentication / Authorization**
   - Geçerli token
   - Süresi dolmuş token
   - Hiç token gönderilmemesi
   - Yetkisi yetmeyen kullanıcı

2. **Veri Doğrulama**
   - Tip uyuşmazlıkları
   - Aralık dışı değerler
   - SQL/NoSQL injection payload'ları
   - XSS payload'ları

3. **Rate Limiting**
   - Limit içinde kalan istekler
   - Limiti aşan istekler
   - Limitin sıfırlanma davranışı

4. **Performans**
   - Cevap süreleri
   - Büyük veri setleriyle davranış
   - Eşzamanlı istekler

`npm test` ile anında çalıştırılabilecek, üretim kalitesinde testler üret.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

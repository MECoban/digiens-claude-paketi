---
description: Görevin karmaşıklığını değerlendirir ve adım adım uygulanabilir bir iş planı çıkarır
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Elinizdeki işi (bug, özellik, refactor vb.) koda dokunmadan önce masaya yatırır: ne kadar süreceğini, nelerin etkileneceğini ve hangi sırayla ilerleneceğini gösteren somut bir plan üretir.

Aşağıda tarif edilen görevi incele ve net, uygulanabilir bir implementasyon planı hazırla.

## Görev

$ARGUMENTS

## Analiz Çerçevesi

### 1. **Görevi Parçalara Ayır**
- Gereksinimleri netleştir
- Bağımlılıkları tespit et
- Etkilenecek dosya ve bileşenleri listele
- Karmaşıklık seviyesini belirle (Küçük / Orta / Büyük)

### 2. **Süre Tahmini**
- **Küçük**: 1-2 saat (basit bug fix, ufak bir özellik)
- **Orta**: Yarım gün - 1 gün (yeni bir component, bir API endpoint'i)
- **Büyük**: 2-5 gün (karmaşık özellik, birden fazla entegrasyon)
- **Çok Büyük**: 1 hafta ve üzeri (kapsamlı refactor, yeni bir alt sistem)

### 3. **Risk Değerlendirmesi**
İşi tıkayabilecek noktaları önceden belirle:
- Henüz bilinmeyen bağımlılıklar
- API kısıtları
- Data migration ihtiyacı
- Breaking change riski
- Üçüncü parti servislerden kaynaklanabilecek sorunlar

### 4. **Uygulama Adımları**

Mantıklı ve sıralı adımlar oluştur:
1. Hazırlık / kurulum
2. Backend değişiklikleri
3. Frontend değişiklikleri
4. Test
5. Dokümantasyon
6. Deployment

### 5. **Başarı Kriterleri**

"Bitti" ne demek, baştan tanımla:
- Özellik tarif edildiği gibi çalışıyor
- Testler geçiyor
- Regression yok
- Kod review'dan geçti
- Dokümante edildi

## Çıktı Formatı

### Görev Analizi
- **Tür**: [Bug Fix / Feature / Refactor / Infrastructure]
- **Karmaşıklık**: [Küçük / Orta / Büyük / Çok Büyük]
- **Tahmini Süre**: X saat/gün
- **Öncelik**: [Yüksek / Orta / Düşük]

### Uygulama Planı

**Faz 1: [İsim]** (süre tahmini)
- [ ] Adım 1
- [ ] Adım 2

**Faz 2: [İsim]** (süre tahmini)
- [ ] Adım 3
- [ ] Adım 4

### Değişecek / Oluşturulacak Dosyalar
```
app/page.tsx (değişecek)
components/YeniComponent.tsx (oluşturulacak)
lib/utils.ts (değişecek)
```

### Bağımlılıklar
```bash
npm install paket-adi
```

### Test Stratejisi
- X için unit test
- Y için integration test
- Elle test adımları

### Olası Sorunlar
- Sorun 1 ve alınacak önlem
- Sorun 2 ve alınacak önlem

### Sonraki Adımlar
1. Faz 1, Adım 1 ile başla
2. Her adımda küçük küçük test et
3. Sık commit at

Karmaşık işi yönetilebilir parçalara bölen, tek kişinin de rahatça takip edebileceği net bir plan sun.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

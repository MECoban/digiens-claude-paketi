---
description: Yeni bir özellik için teknik tasarım ve uygulama planı hazırlar
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Aklınızdaki yeni özelliği kod yazmaya başlamadan önce planlar: hangi dosyalar değişecek, hangi teknolojiler kullanılacak, hangi sırayla ilerlenecek ve riskler neler — hepsini tek bir yol haritasında toplar.

Aşağıda tarif edilen özellik için detaylı bir implementasyon planı oluştur.

## Özellik Tanımı

$ARGUMENTS

## Planlama Çerçevesi

### 1. **Özelliği Parçalara Ayır**

Şunları çıkararak analiz et:
- User story'ler
- Teknik gereksinimler
- Bağımlılıklar
- Edge case'ler
- Başarı kriterleri

### 2. **Teknik Şartname**

**Mimari**
- Bu özellik codebase'in neresine oturuyor?
- Hangi component ve sayfalar etkilenecek?
- Yeni dosyalar mı, mevcut dosyalarda değişiklik mi?
- Database schema değişikliği gerekiyor mu?
- Hangi API endpoint'lerine ihtiyaç var?

**Teknoloji Seçimleri**
- Gereken kütüphane/paketler
- Her seçimin gerekçesi
- Değerlendirilen alternatifler
- Ödünler (trade-off)

**Veri Akışı**
```
Kullanıcı Aksiyonu → Frontend → API → Database → Yanıt
```

### 3. **Uygulama Adımları**

Mantıklı ve sıralı görevlere böl:

1. **Kurulum** — bağımlılıklar, konfigürasyon
2. **Database** — schema, migration'lar, RLS policy'leri
3. **Backend** — API route'ları, validasyon, iş mantığı
4. **Frontend** — component'ler, sayfalar, formlar
5. **Entegrasyon** — parçaları birbirine bağla
6. **Test** — unit, integration, E2E
7. **Cila** — hata yönetimi, loading state'leri, UX

### 4. **Risk Değerlendirmesi**

Olası sorunları önceden belirle:
- **Teknik Riskler** — karmaşıklık, daha önce girilmemiş alanlar
- **Zaman Riskleri** — küçümsenen görevler
- **Bağımlılık Riskleri** — harici API'ler, üçüncü parti servisler
- **Veri Riskleri** — migration, geriye dönük uyumluluk

### 5. **Süre Tahmini**

Gerçekçi tahminler ver:
- Küçük görev: 1-2 saat
- Orta görev: yarım gün
- Büyük görev: 1-2 gün
- Karmaşık görev: 3-5 gün

**Altın kural**: Tek başına geliştiriyorsan ilk tahminini ikiyle çarp.

### 6. **Başarı Kriterleri**

"Bitti"yi baştan tanımla:
- Özellik tarif edildiği gibi çalışıyor
- Testler geçiyor
- Console'da hata yok
- Erişilebilir (accessible)
- Responsive
- Hata yönetimi var
- Loading state'leri var
- Dokümantasyon güncellendi

## Çıktı Formatı

### 1. **Özelliğe Genel Bakış**
- Hangi problemi çözüyor?
- Kimin için?
- Ana işlevler neler?

### 2. **Teknik Tasarım**
```
┌──────────┐    ┌──────┐    ┌──────────┐
│ Frontend │ →  │ API  │ →  │ Database │
└──────────┘    └──────┘    └──────────┘
```
- Component yapısı
- API endpoint'leri
- Database schema
- State yönetimi

### 3. **Uygulama Planı**

**Faz 1: Temel** (1. gün)
- [ ] Görev 1
- [ ] Görev 2

**Faz 2: Ana Özellik** (2-3. gün)
- [ ] Görev 3
- [ ] Görev 4

**Faz 3: Cila** (4. gün)
- [ ] Görev 5
- [ ] Görev 6

### 4. **Dosya Değişiklikleri**

**Yeni Dosyalar**
```
app/api/ozellik/route.ts
components/OzellikComponent.tsx
lib/ozellik-utils.ts
```

**Değişecek Dosyalar**
```
app/page.tsx (yeni bölüm eklenecek)
lib/database.types.ts (yeni tipler eklenecek)
```

### 5. **Bağımlılıklar**

**Kurulacak npm paketleri**
```bash
npm install paket-adi
```

**Environment değişkenleri**
```bash
FEATURE_API_KEY=xxx
```

### 6. **Test Stratejisi**

- Utility'ler için unit test
- API için integration test
- UI için component test
- Uçtan uca akış için E2E test

### 7. **Yayına Alma Planı**

- Gerekiyorsa feature flag
- Kademeli açılış stratejisi
- Geri alma (rollback) planı
- İzleme ve metrikler

### 8. **Sonraki Adımlar**

1. Planı gözden geçir
2. Ortamı hazırla
3. Faz 1 ile başla
4. Her adımda test et
5. Staging'e çıkar
6. Production'a al

Tek bir geliştiricinin dahi adım adım takip edebileceği, net ve uygulanabilir bir plan sun.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

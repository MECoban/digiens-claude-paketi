---
description: Kodu performans, bellek kullanımı ve verimlilik açısından inceleyip hızlandırır
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Yavaş çalışan veya gereksiz kaynak tüketen kodu inceler; darboğazı bulur, hızlandırılmış bir sürüm önerir ve neyin neden değiştiğini açıklar.

Aşağıdaki kodu performans ve verimlilik açısından optimize et.

## Optimize Edilecek Kod

$ARGUMENTS

## Optimizasyon Stratejisi

### 1. **Önce Ölç, Sonra Optimize Et**
- Gerçek darboğazı profiling ile tespit et
- Erken optimizasyona (premature optimization) girme
- Değişiklik öncesi ve sonrasını ölçerek karşılaştır
- Etkisi en yüksek alanlara odaklan

### 2. **Performans Optimizasyon Alanları**

**React/Next.js**
- Memoization (React.memo, useMemo, useCallback)
- Code splitting ve lazy loading
- Görsel optimizasyonu (next/image)
- Font optimizasyonu (next/font)
- Gereksiz re-render'ları ayıkla
- Uzun listelerde virtual scrolling

**Veritabanı Sorguları**
- Sık sorgulanan alanlara index ekle
- Sorguları batch'le (N+1 problemini çöz)
- select ile yalnızca gereken alanları çek
- Pagination uygula
- Sık çalışan sorguları cache'le
- Karmaşık join'ler için database view kullan

**API Çağrıları**
- Caching kur (SWR, React Query)
- İstekleri debounce/throttle et
- Mümkün olan yerde istekleri paralel at
- Aynı isteğin tekrarını engelle (request deduplication)
- Optimistic update uygula

**Bundle Boyutu**
- Kullanılmayan kodu tree-shaking ile at
- Büyük kütüphaneleri dynamic import ile yükle
- Ağır bağımlılıkları hafif alternatiflerle değiştir
- Route bazlı code splitting
- Ekranın altında kalan içeriği lazy load et

**Bellek**
- Memory leak'leri kapat (useEffect cleanup)
- Gereksiz nesne üretiminden kaçın
- Değişmeyen değerlere const kullan
- interval/timeout'ları temizle
- Event listener'ları kaldır

### 3. **Optimizasyon Kontrol Listesi**

**JavaScript/TypeScript**
- var yerine const/let
- Mümkünse iç içe döngülerden kaçın
- Lookup için Map/Set kullan
- DOM manipülasyonunu en aza indir
- Pahalı işlemleri debounce/throttle et

**React**
- Sık render olan component'leri memo'la
- Statik değerleri component dışına taşı
- Listelerde key'leri doğru kullan
- Render içinde inline fonksiyon tanımlama
- Route ve component'leri lazy load et

**Next.js**
- Mümkün olan her yerde Server Component kullan
- Dinamik içerik için ISR uygula
- Görselleri next/image ile servis et
- Kritik route'ları prefetch et
- Streaming için Suspense kullan

**Veritabanı**
- Foreign key'lere index koy
- Prepared statement kullan
- Insert/update işlemlerini batch'le
- Connection pooling kur
- Pahalı sorguları cache'le

**Ağ**
- Yanıtları sıkıştır (gzip/brotli)
- Statik dosyalar için CDN kullan
- HTTP/2 aç
- Doğru cache header'ları ayarla
- Payload boyutunu küçült

### 4. **Ölçüm Araçları**

**Frontend**
- Chrome DevTools Performance sekmesi
- Lighthouse CI
- React DevTools Profiler
- Bundle Analyzer (next/bundle-analyzer)

**Backend**
- Node.js profiler
- Veritabanı query analyzer
- APM araçları (DataDog, New Relic)
- Yük testi (k6, Artillery)

### 5. **Sık Kullanılan Optimizasyonlar**

**Verimsiz array zincirini tek geçişe indir**
```typescript
// Önce: dizi üç kez dolaşılıyor
const sonuc = dizi
  .filter(x => x > 0)
  .map(x => x * 2)
  .reduce((toplam, x) => toplam + x, 0)

// Sonra: tek geçiş yeterli
const sonuc = dizi.reduce((toplam, x) => {
  return x > 0 ? toplam + (x * 2) : toplam
}, 0)
```

**Pahalı hesaplamayı memoize et**
```typescript
const pahaliDeger = useMemo(() => {
  return karmasikHesap(props.data)
}, [props.data])
```

**Uzun listelerde virtual scrolling**
```typescript
import { useVirtual } from 'react-virtual'
// Yalnızca ekranda görünen satırlar render edilir
```

## Çıktı Formatı

1. **Analiz** — tespit edilen performans darboğazları
2. **Optimize Edilmiş Kod** — iyileştirilmiş sürüm
3. **Açıklama** — ne değişti, neden değişti
4. **Beklenen Kazanım** — tahmini performans iyileşmesi
5. **Ödünler (Trade-off)** — eklenen karmaşıklık varsa belirt
6. **Sonraki Adımlar** — başka hangi optimizasyonlar mümkün

Kullanıcıya gerçekten hissedilir fayda sağlayan, ölçülebilir optimizasyonlara odaklan. Mikro-optimizasyon uğruna okunabilirlikten ödün verme.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

---
description: App Router kalıplarıyla yeni bir Next.js sayfası oluşturur (loading, error ve SEO dahil)
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Sitenize/uygulamanıza yeni bir sayfa ekler; sadece görünen kısmı değil, yüklenme ekranını, hata durumunu ve Google'da doğru görünmesini sağlayan SEO ayarlarını da tek seferde hazırlar.

Aşağıdaki tarife göre, App Router kalıplarına uygun bir Next.js 15 sayfası oluştur.

## Sayfa Tarifi

$ARGUMENTS

## Next.js 15 App Router Standartları

### 1. **Dosya Düzeni**
```
app/
   [route]/
      page.tsx          # Ana sayfa component'i
      layout.tsx        # Layout (opsiyonel)
      loading.tsx       # Yüklenme arayüzü
      error.tsx         # Hata arayüzü
      not-found.tsx     # 404 arayüzü
```

### 2. **Varsayılan: Server Component**
- Veri doğrudan component içinde çekilir
- getServerSideProps / getStaticProps devri kapandı
- Async component desteklenir
- Daha iyi performans

### 3. **Metadata**
```typescript
export const metadata: Metadata = {
  title: 'Sayfa Başlığı',
  description: 'SEO için sayfa açıklaması',
  openGraph: { /* OG etiketleri */ }
}
```

### 4. **Veri Çekme Kalıpları**

**Server Component** (tercih edilen)
```typescript
async function Page() {
  const data = await fetchData()
  return <div>{data}</div>
}
```

**Client Component** (gerektiğinde)
```typescript
'use client'
function Page() {
  const { data } = useSWR('/api/data')
  return <div>{data}</div>
}
```

## Üretilecekler

1. **Sayfa Component'i** — `app/[route]/page.tsx`
2. **TypeScript Tipleri** — props ve veri tipleri
3. **Yüklenme Durumu** — `loading.tsx`
4. **Error Boundary** — `error.tsx` (App Router'da bu dosya Client Component olmak ZORUNDADIR, başına `'use client'` koy)
5. **Metadata** — SEO ve OG etiketleri
6. **Veri Çekme Örneği** — server veya client kalıbı

## Sayfa Kalıpları

**Statik Sayfa** (varsayılan)
- Build sırasında önceden render edilir
- Pazarlama sayfaları ve bloglar için ideal
- En hızlı seçenek

**Belirli Aralıklarla Yenilenen Sayfa**
```typescript
export const revalidate = 60 // 60 saniyede bir yeniden doğrula
```

**Dinamik Route** (`[slug]`)
```typescript
export async function generateStaticParams() {
  // Path'leri build sırasında üret
}
```

**Streaming** (Suspense ile)
```typescript
<Suspense fallback={<Loading />}>
  <AsyncComponent />
</Suspense>
```

## Uyulacak İlkeler

**Yapı**
- ✅ Veri çekme işi Server Component'lerde
- ✅ Client Component sadece gerektiğinde ('use client')
- ✅ Yavaş veri için Suspense ile streaming
- ✅ Paralel veri çekme
- ✅ Eksiksiz TypeScript tipleri

**Performans**
- ✅ Görsel optimizasyonu (next/image)
- ✅ Font optimizasyonu (next/font)
- ✅ Ekranın altında kalan içerikte lazy loading
- ✅ Otomatik code splitting
- ✅ Link prefetch (varsayılan davranış)

**SEO**
- ✅ Her sayfada metadata
- ✅ Semantik HTML
- ✅ Open Graph etiketleri
- ✅ Yapılandırılmış veri (JSON-LD)
- ✅ Görsellerde alt metni

**Hata Yönetimi**
- ✅ Çalışma zamanı hataları için error.tsx
- ✅ 404 için not-found.tsx
- ✅ Zarif düşüş (graceful degradation)
- ✅ Kullanıcıya anlaşılır hata mesajları

**Erişilebilirlik**
- ✅ Semantik HTML5 elemanları
- ✅ ARIA etiketleri
- ✅ Klavye ile gezinme
- ✅ Focus yönetimi

## 'use client' Ne Zaman Gerekir?

Şunlara ihtiyaç varsa Client Component kullan:
- Event listener'lar (onClick, onChange vb.)
- State hook'ları (useState, useReducer)
- Effect hook'ları (useEffect, useLayoutEffect)
- Sadece tarayıcıda çalışan API'ler (localStorage, window)
- Yukarıdakileri kullanan custom hook'lar

Bunların hiçbiri yoksa varsayılanı koru: Server Component.

## Stil Entegrasyonu

Projeye göre seç:
- **Tailwind CSS** — utility sınıfları (önerilen)
- **CSS Modules** — scope'lu stiller
- **Styled Components** — CSS-in-JS ('use client' gerektirir)

TypeScript tipleri, hata yönetimi ve SEO optimizasyonu tamam olan, üretime hazır komple bir sayfa üret.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

---
description: TypeScript ve güncel React kalıplarıyla yeni bir component oluşturur
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Arayüzünüz için yeni bir yapı taşı (buton, kart, form, liste gibi tekrar kullanılabilir bir parça) üretir; kodun tipli, erişilebilir ve projenin geri kalanıyla uyumlu olmasını baştan garanti eder.

Aşağıdaki tarife göre, güncel standartlara uygun bir React component'i oluştur.

## Component Tarifi

$ARGUMENTS

## React + TypeScript Standartları

### 1. **Sadece Function Component**
- Class component yok, function component var
- React 19 kalıpları
- Next.js'te uygun yerlerde Server Component

### 2. **TypeScript Kuralları**
- Strict mod (`strict: true`)
- Props için interface tanımı
- Yerleşik utility tipler (ComponentProps, ReactNode vb.)
- `any` KESİNLİKLE yok
- Karmaşık component'lerde açık dönüş tipi

### 3. **Component Kalıpları**

**Client Component** (etkileşimli, hook kullanan)
```typescript
'use client'
import { useState } from 'react'

interface Props {
  // tipli props
}

export function Component({ }: Props) {
  // implementasyon
}
```

**Server Component** (Next.js App Router'da varsayılan)
```typescript
interface Props {
  // tipli props
}

export async function Component({ }: Props) {
  // veriyi doğrudan burada çekebilir
}
```

### 4. **State Yönetimi**
- Yerel state → `useState`
- Karmaşık state → `useReducer`
- Global state → Zustand
- Tema / auth gibi kesitler → React Context

### 5. **Performans**
- `React.lazy()` ile lazy loading
- Code splitting
- Pahalı hesaplamalarda `useMemo()`
- Callback'lerde `useCallback()`

### 6. **Stil Yaklaşımı** (projeye göre)
- **Tailwind CSS** — utility-first (önerilen)
- **CSS Modules** — scope'lu stiller
- **Styled Components** — CSS-in-JS

## Üretilecekler

1. **Component Dosyası** — TypeScript ile ana component
2. **Props Interface** — eksiksiz tiplenmiş props
3. **Stiller** — Tailwind sınıfları veya CSS module
4. **Kullanım Örneği** — nasıl import edilip kullanılacağı
5. **Storybook Story** (opsiyonel) — component dokümantasyonu

## Kalite Standartları

**Yapı**
- ✅ Feature bazlı klasör düzeni
- ✅ İlgili dosyalar yan yana (co-location)
- ✅ Barrel export (index.ts)
- ✅ Tutarlı dosya isimlendirme

**TypeScript**
- ✅ Interface ile açık prop tipleri
- ✅ Gerektiğinde generic kullanımı
- ✅ Utility tipler (Pick, Omit, Partial)
- ✅ Varyantlar için discriminated union

**Props**
- ✅ Zorunlu / opsiyonel ayrımı net
- ✅ Uygun yerlerde varsayılan değer
- ✅ Fonksiyon imzasında destructure
- ✅ Props spread'i dikkatli kullan

**Erişilebilirlik**
- ✅ Semantik HTML
- ✅ Gereken yerde ARIA etiketleri
- ✅ Klavye ile gezinebilirlik
- ✅ Ekran okuyucu dostu

**Genel İlkeler**
- ✅ Tek sorumluluk ilkesi
- ✅ Kalıtım yerine kompozisyon
- ✅ Karmaşık mantığı custom hook'a çıkar
- ✅ Component'i küçük tut (200 satırın altı)

## Değerlendirilecek Component Türleri

**Presentational Component**
- Saf arayüz çizimi
- İş mantığı yok
- Veriyi props ile alır
- Test etmesi kolay

**Container Component**
- Veri çekme
- İş mantığı
- State yönetimi
- Veriyi presentational component'lere aktarır

**Compound Component**
- Birlikte çalışan ilişkili parçalar
- Paylaşılan context
- Esnek API
- Örnek: `<Select><Select.Trigger/><Select.Content/></Select>`

## Kullanılabilecek React 19 Özellikleri

- **use()** — promise ve context okumak için
- **useActionState()** — form state'i için
- **useFormStatus()** — form pending durumu için
- **useOptimistic()** — iyimser UI güncellemeleri için
- **Server Actions** — mutation'lar için

Next.js 15 ve React 19 kalıplarına uyan; üretime hazır, erişilebilir ve performanslı bir component üret.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

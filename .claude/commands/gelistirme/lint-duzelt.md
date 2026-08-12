---
description: Lint araçlarını çalıştırır ve kod kalitesi sorunlarını düzeltir
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Projedeki kod kalitesi kontrollerini (lint, tip denetimi, biçimlendirme) çalıştırır; otomatik düzeltilebilenleri düzeltir, elle müdahale gerekenleri önem sırasına göre listeler.

Codebase'de lint kontrollerini çalıştır ve kod kalitesi sorunlarını gider.

## Hedef

$ARGUMENTS

## Lint Stratejisi

### 1. **Lint Komutlarını Çalıştır**

```bash
# ESLint (JavaScript/TypeScript)
npm run lint
npx eslint . --fix

# TypeScript derleyici kontrolü
npx tsc --noEmit

# Prettier (biçimlendirme)
npx prettier --write .

# Hepsi bir arada
npm run lint && npx tsc --noEmit && npx prettier --write .
```

### 2. **Sık Görülen ESLint Sorunları**

**TypeScript Hataları**
- Eksik tip anotasyonları
- `any` kullanımı
- Kullanılmayan değişkenler
- Eksik return tipleri

**React/Next.js Sorunları**
- Listelerde eksik key
- Güvensiz useEffect dependency'leri
- JSX içinde kaçış yapılmamış (unescaped) karakterler
- Görsellerde eksik alt metni

**Kod Kalitesi**
- Kullanılmayan import'lar
- Unutulmuş console.log'lar
- Debugger ifadeleri
- Bekleyen TODO yorumları

**İyi Pratikler**
- var yerine const/let
- Mümkünse let yerine const
- İç içe ternary'lerden kaçın
- Tutarlı return ifadeleri

### 3. **Otomatik Düzeltilebilenleri Düzelt**

**Güvenli Otomatik Düzeltmeler**
```bash
# Biçimlendirmeyi düzelt
prettier --write .

# ESLint'in otomatik düzeltebildiği kuralları uygula
eslint --fix .

# Import sıralamasını düzelt
eslint --fix --rule 'import/order: error' .
```

**Elle Düzeltme Gerektirenler**
- Tip anotasyonları
- Mantık hataları
- Eksik hata yönetimi
- Erişilebilirlik (accessibility) sorunları

### 4. **Lint Konfigürasyonu**

**ESLint** (`.eslintrc.json`)
```json
{
  "extends": [
    "next/core-web-vitals",
    "plugin:@typescript-eslint/recommended"
  ],
  "rules": {
    "@typescript-eslint/no-explicit-any": "error",
    "@typescript-eslint/no-unused-vars": "error",
    "no-console": "warn"
  }
}
```

**Prettier** (`.prettierrc`)
```json
{
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5"
}
```

### 5. **Düzeltme Öncelikleri**

**Yüksek Öncelik** (hemen düzelt)
- Build'i kıran tip hataları
- Güvenlik açıkları
- Runtime hataları
- Bozuk erişilebilirlik

**Orta Öncelik** (commit'ten önce düzelt)
- Eksik tip anotasyonları
- Kullanılmayan değişkenler
- Kod stili ihlalleri
- TODO yorumları

**Düşük Öncelik** (fırsat bulunca düzelt)
- Biçimlendirme tutarsızlıkları
- Yorum iyileştirmeleri
- Küçük refactor fırsatları

### 6. **Pre-Commit Hook'ları** (Tavsiye Edilir)

**Husky + lint-staged kurulumu**
```bash
npm install -D husky lint-staged
npx husky init
```

**Yapılandırma** (`.husky/pre-commit`)
```bash
npx lint-staged
```

**lint-staged ayarı** (`package.json`)
```json
{
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ]
  }
}
```

### 7. **VS Code Entegrasyonu**

**Ayarlar** (`.vscode/settings.json`)
```json
{
  "editor.formatOnSave": true,
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "typescript.tsdk": "node_modules/typescript/lib"
}
```

## Üretilecek Çıktılar

1. **Lint Raporu** — bulunan tüm sorunlar
2. **Otomatik Düzeltme Sonuçları** — nelerin kendiliğinden düzeltildiği
3. **Elle Düzeltme Önerileri** — müdahale gerektiren sorunlar
4. **Öncelik Listesi** — önem derecesine göre sıralı
5. **Konfigürasyon Önerileri** — lint kurulumunu güçlendirecek ayarlar

## Tipik Düzeltmeler

**Kullanılmayan Import'u Kaldır**
```typescript
// Önce
import { A, B, C } from 'lib'

// Sonra
import { A, C } from 'lib'  // B kullanılmıyordu
```

**Tip Anotasyonu Ekle**
```typescript
// Önce
function isle(data) {
  return data.map(x => x.value)
}

// Sonra
function isle(data: DataItem[]): number[] {
  return data.map(x => x.value)
}
```

**Eksik Key'i Tamamla**
```typescript
// Önce
{items.map(item => <div>{item.name}</div>)}

// Sonra
{items.map(item => <div key={item.id}>{item.name}</div>)}
```

Kod kalitesini yükselten ve bug'ları henüz oluşmadan engelleyen düzeltmelere odaklan. Her commit'ten önce lint çalıştırmayı alışkanlık haline getir.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

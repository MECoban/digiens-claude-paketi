---
description: Supabase veritabanı şemasından TypeScript tipleri üretir
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Veritabanınızdaki tabloların yapısını okuyup koda "tip" olarak aktarır. Böylece tabloya uymayan bir veri yazmaya kalktığınızda hatayı uygulama çöktükten sonra değil, daha kod yazarken görürsünüz.

Supabase şemasından TypeScript tiplerini üret ve projeye bağla.

## Temel Komut

Tipleri üretmek için:

```bash
npx supabase gen types typescript --project-id YOUR_PROJECT_ID > lib/database.types.ts
```

Yerel (local) Supabase kullanıyorsan:

```bash
npx supabase gen types typescript --local > lib/database.types.ts
```

## Otomatikleştirme Kurulumu

### 1. **package.json'a script ekle**

```json
{
  "scripts": {
    "gen-types": "npx supabase gen types typescript --project-id $SUPABASE_PROJECT_ID > lib/database.types.ts",
    "gen-types:local": "npx supabase gen types typescript --local > lib/database.types.ts"
  }
}
```

### 2. **Kodda kullanım**

```typescript
import type { Database } from '@/lib/database.types'

// Tablo tiplerini çıkar
type User = Database['public']['Tables']['users']['Row']
type UserInsert = Database['public']['Tables']['users']['Insert']
type UserUpdate = Database['public']['Tables']['users']['Update']

// Supabase client'ı tiple
const supabase = createClient<Database>(url, key)

// Tip güvenli sorgu
const { data } = await supabase
  .from('users')
  .select('*')
  .single()  // data artık User tipinde

// Tip güvenli insert
const { data } = await supabase
  .from('users')
  .insert({
    email: 'user@example.com',
    name: 'John Doe'
  })  // Şekli TypeScript denetler
```

### 3. **Yardımcı tipler oluştur**

```typescript
// lib/database.helpers.ts
import type { Database } from './database.types'

// Tablo tiplerine kısayol
export type Tables<T extends keyof Database['public']['Tables']> =
  Database['public']['Tables'][T]['Row']

export type Enums<T extends keyof Database['public']['Enums']> =
  Database['public']['Enums'][T]

// Kullanımı
import type { Tables } from '@/lib/database.helpers'
type User = Tables<'users'>
type Post = Tables<'posts'>
```

### 4. **Ne zaman yeniden üretmeli?**

Şu değişikliklerden sonra `npm run gen-types` çalıştır:
- Yeni tablo oluşturduğunda
- Kolon eklediğinde / sildiğinde
- Kolon tipini değiştirdiğinde
- Veritabanı fonksiyonu veya view eklediğinde/değiştirdiğinde
- Enum eklediğinde

Not: RLS policy'leri üretilen tipleri DEĞİŞTİRMEZ (tipler şemadan gelir); policy değişikliği sonrası yeniden üretim gerekmez.

### 5. **Kurallar**

- ✅ Üretilen tip dosyasını git'e commit'le
- ✅ Her şema değişikliğinden sonra yeniden üret
- ✅ Tüm Supabase sorgularında bu tipleri kullan
- ✅ Sık kullanılan kalıplar için helper tipler yaz
- ✅ Tip dosyasını `lib/` veya `types/` altında tut
- ❌ Üretilen dosyayı elle düzenleme
- ❌ Üretilen tipler dururken `any` kullanma

### 6. **Pre-commit hook ile entegrasyon**

```bash
# .husky/pre-commit
#!/bin/sh
npm run gen-types
git add lib/database.types.ts
```

## Sorun Giderme

**Sorun**: `supabase` komutu bulunamıyor
```bash
npm install -g supabase
```

**Sorun**: Project ID eksik
```bash
# Project ID'yi Supabase dashboard'da bulabilirsin
# ya da .env dosyasına yaz:
SUPABASE_PROJECT_ID=your-project-id
```

**Sorun**: Tipler güncellenmiyor
```bash
# Eski dosyayı sil ve yeniden üret
rm lib/database.types.ts
npm run gen-types
```

Amaç: veritabanı kaynaklı hataları runtime'da değil, derleme aşamasında yakalamak.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

---
description: Kod, API ve component'ler için dokümantasyon üretir
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Verdiğiniz kod için dokümantasyon hazırlar: fonksiyon açıklamaları, API tanımları, component prop'ları ve README bölümleri — ileride kodu açan kişinin (siz dahil) hızla anlamasını sağlayacak şekilde.

Aşağıdaki kod için kapsamlı dokümantasyon üret.

## Dokümante Edilecek Kod

$ARGUMENTS

## Dokümantasyon Stratejisi

### 1. **Dokümantasyon Türleri**

**Kod Dokümantasyonu**
- JSDoc/TSDoc yorumları
- Fonksiyon/metod açıklamaları
- Parametre açıklamaları
- Return tipleri ve değerleri
- Kullanım örnekleri

**API Dokümantasyonu**
- Endpoint açıklamaları
- Request/response formatları
- Authentication gereksinimleri
- Hata kodları
- curl/fetch örnekleri

**Component Dokümantasyonu**
- Props interface'i
- Kullanım örnekleri
- Görsel örnekler
- Erişilebilirlik notları

**README Dokümantasyonu**
- Proje özeti
- Kurulum adımları
- Environment değişkenleri
- Mevcut script'ler
- Deployment rehberi

### 2. **JSDoc/TSDoc Formatı**

```typescript
/**
 * Veritabanından kullanıcı verisini getirir
 *
 * @param userId - Kullanıcının benzersiz kimliği
 * @param options - İsteğe bağlı sorgu parametreleri
 * @returns Kullanıcı verisine çözümlenen Promise
 * @throws {NotFoundError} Kullanıcı bulunamadığında
 * @throws {DatabaseError} Veritabanı sorgusu başarısız olduğunda
 *
 * @example
 * ```typescript
 * const user = await getUser('123', { includeProfile: true })
 * console.log(user.email)
 * ```
 */
async function getUser(
  userId: string,
  options?: FetchOptions
): Promise<User> {
  // implementasyon
}
```

### 3. **API Dokümantasyonu**

```markdown
## POST /api/users

Yeni bir kullanıcı hesabı oluşturur.

### Authentication
`Authorization` header'ında geçerli bir API key gerektirir.

### Request Body
```json
{
  "email": "user@example.com",
  "name": "Ayşe Yılmaz",
  "role": "user"
}
```

### Yanıt (201 Created)
```json
{
  "id": "user_123",
  "email": "user@example.com",
  "name": "Ayşe Yılmaz",
  "createdAt": "2025-01-01T00:00:00Z"
}
```

### Hatalar
- `400` — Geçersiz request body
- `401` — Eksik veya geçersiz API key
- `409` — E-posta zaten kayıtlı
- `500` — Sunucu hatası

### Örnek
```bash
curl -X POST https://api.example.com/api/users \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","name":"Ayşe Yılmaz"}'
```
```

### 4. **Component Dokümantasyonu**

```typescript
/**
 * UserCard Component'i
 *
 * Kullanıcı bilgisini kart düzeninde gösterir: avatar,
 * isim, e-posta ve isteğe bağlı aksiyon butonları.
 *
 * @component
 * @example
 * ```tsx
 * <UserCard
 *   user={userData}
 *   onEdit={() => handleEdit(userData.id)}
 *   showActions={true}
 * />
 * ```
 */
interface UserCardProps {
  /** Gösterilecek kullanıcı verisi */
  user: User

  /** Düzenle butonuna tıklandığında çağrılan opsiyonel callback */
  onEdit?: () => void

  /** Aksiyon butonları gösterilsin mi (varsayılan: false) */
  showActions?: boolean

  /** Ek CSS class'ları */
  className?: string
}

export function UserCard({
  user,
  onEdit,
  showActions = false,
  className
}: UserCardProps) {
  // implementasyon
}
```

### 5. **README Şablonu**

```markdown
# Proje Adı

Projenin ne yaptığını anlatan kısa açıklama.

## Özellikler

- Özellik 1
- Özellik 2
- Özellik 3

## Teknoloji Yığını

- Next.js 15
- React 19
- TypeScript
- Tailwind CSS
- Supabase

## Başlarken

### Ön Koşullar

- Node.js 18+
- npm veya pnpm

### Kurulum

```bash
# Repoyu klonla
git clone https://github.com/kullanici/proje.git

# Bağımlılıkları kur
npm install

# Environment değişkenlerini hazırla
cp .env.example .env.local
```

### Environment Değişkenleri

```bash
DATABASE_URL=           # Supabase database URL'i
NEXT_PUBLIC_API_URL=    # API endpoint'i
```

### Geliştirme

```bash
npm run dev            # Geliştirme sunucusunu başlat
npm run build          # Production build al
npm run start          # Production sunucusunu başlat
npm test               # Testleri çalıştır
npm run lint           # Lint çalıştır
```

## Proje Yapısı

```
   app/                # Next.js app dizini
   components/         # React component'leri
   lib/                # Yardımcı fonksiyonlar
   types/              # TypeScript tipleri
   public/             # Statik dosyalar
```

## Deployment

Vercel üzerinde barındırılıyor. `main` branch'ine push otomatik deploy tetikler.

## Lisans

MIT
```

### 6. **Satır İçi Dokümantasyon İlkeleri**

**İyi Yorumlar**
```typescript
// Pahalı hesaplamayı 5 dakikalığına cache'le
const cachedResult = useMemo(() =>
  complexCalculation(data), [data]
)

// Başarısız istekleri exponential backoff ile en fazla 3 kez tekrarla
const result = await retry(apiCall, { maxAttempts: 3 })
```

**Kötü Yorumlar** (barizi belgelemeyin)
```typescript
// x'i 5 yap
const x = 5

// Elemanları dolaş
items.forEach(item => { })
```

### 7. **Otomatik Üretilen Dokümanlar**

**TypeDoc** (TypeScript projeleri için)
```bash
npm install -D typedoc
npx typedoc --out docs src
```

**Storybook** (React component'leri için)
```bash
npx storybook@latest init
npm run storybook
```

## Üretilecek Çıktılar

1. **JSDoc Yorumları** — export edilen tüm fonksiyon ve class'lar için
2. **README Bölümü** — projeyle ilgili dokümantasyon
3. **API Dokümanları** — API route'ları varsa
4. **Component Prop'ları** — açıklamalı TypeScript interface'i
5. **Kullanım Örnekleri** — gerçek dünyadan kod örnekleri
6. **Sorun Giderme** — sık karşılaşılan sorunlar ve çözümleri

Gelecekteki sizin (veya başka bir geliştiricinin) kodu hızla anlayıp kullanmasını sağlayacak dokümantasyona odaklan. Zaten bariz olanı belgeleme.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

---
description: Doğrulama, hata yönetimi ve TypeScript ile üretime hazır yeni bir Next.js API route oluşturur
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Uygulamanızın sunucu tarafına yeni bir "kapı" (API endpoint) açar: dışarıdan gelen isteği karşılayan, gelen veriyi kontrol eden ve düzgün cevap dönen kodu sizin yerinize, kurallara uygun şekilde hazırlar.

Aşağıda tarif edilen endpoint için, modern standartlara uygun ve tek başına geliştirme yapan biri için bakımı kolay bir Next.js API route'u oluştur.

## İstenen Endpoint

$ARGUMENTS

## Uygulama Kuralları

### 1. **Next.js 15 App Router**
Route Handler'ları `app/api/` dizini altında, TypeScript ile yaz.

### 2. **Girdi Doğrulama**
- Runtime doğrulama için Zod kullan
- Doğrulamayı EN BAŞTA yap — veritabanına ya da dış servise gitmeden önce
- Doğrulama hatalarında kullanıcıya ne yanlış gittiğini net söyle

### 3. **Hata Yönetimi**
- try/catch ile merkezi hata yakalama
- Tüm endpoint'lerde aynı hata cevap formatı
- Duruma uygun HTTP status kodları
- Hassas hata detaylarını (stack trace, iç mesajlar) dışarı sızdırma

### 4. **TypeScript**
- Request ve response için katı tipler
- Ortak tip tanımları tek yerde
- `any` kullanımı yasak

### 5. **Güvenlik**
- Girdi temizliği (sanitization)
- Gerekiyorsa CORS ayarı
- Rate limiting ihtiyacını değerlendir
- Authentication / authorization kontrolleri

### 6. **Cevap Formatı**
```typescript
// Başarılı
{ data: T, success: true }

// Hatalı
{ error: string, details?: unknown, success: false }
```

## Üretilecek Parçalar

Eksiksiz bir API route şu dosyalardan oluşur:

1. **Route Handler** — `app/api/[route]/route.ts`
2. **Doğrulama Şeması** — request/response için Zod şemaları
3. **Tip Tanımları** — paylaşılan TypeScript tipleri
4. **Hata Yakalayıcı** — merkezi error handler
5. **Kullanım Örneği** — client tarafından fetch ile çağrı örneği

## Uyulacak İlkeler

- ✅ Pahalı işlemlerden (DB, dış API) önce erken doğrulama
- ✅ Doğru HTTP status kodları (200, 201, 400, 401, 404, 500)
- ✅ Tutarlı hata cevap formatı
- ✅ TypeScript strict mode
- ✅ Route içinde minimum mantık — asıl işi service/util katmanına taşı
- ✅ Environment variable'ların varlığını doğrula
- ✅ Debug için request/response logging
- ❌ Cevaplarda hassas veri olmaz
- ❌ Doğrulanmamış girdiyle veritabanı sorgusu olmaz
- ❌ Route içine gömülü iş mantığı olmaz (service'e çıkar)

Projeye kopyalandığı anda çalışacak, üretime hazır kod üret.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

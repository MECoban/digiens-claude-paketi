---
description: Var olan bir API endpoint'ine authentication, authorization ve güvenlik katmanları ekler
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Herkese açık duran bir API kapısına kilit takar: isteği yapanın kim olduğunu doğrular, o işlemi yapmaya yetkisi var mı diye bakar ve kötü niyetli istekleri (saldırı, spam, aşırı yüklenme) daha kapıda durdurur.

Aşağıda belirtilen API route'una kapsamlı güvenlik, kimlik doğrulama ve yetkilendirme ekle.

## Hedef API Route

$ARGUMENTS

## Eklenecek Güvenlik Katmanları

### 1. **Authentication** — "Sen kimsin?"
- Kullanıcı kimliğinin doğrulanması
- Token kontrolü (JWT, session veya API key)
- Süresi dolmuş / geçersiz token'ların ele alınması

### 2. **Authorization** — "Bunu yapmaya yetkin var mı?"
- Rol tabanlı erişim kontrolü (RBAC)
- Kaynak seviyesinde izinler
- Kaydın gerçekten o kullanıcıya ait olduğunun kontrolü (ownership)

### 3. **Girdi Doğrulama**
- Tüm girdilerin temizlenmesi
- SQL/NoSQL injection önlemleri
- XSS önlemleri
- Zod ile tip doğrulama

### 4. **Rate Limiting**
- Kötüye kullanımı engelle
- Kullanıcı ve/veya IP başına limit
- Sliding window algoritması

### 5. **CORS** (gerekiyorsa)
- Sadece izinli origin'lere açık whitelist
- Doğru header'lar
- Credential yönetimi

## Projeye Göre Yaklaşım

### Supabase kullanan projede:
```typescript
// Supabase Auth + RLS ikilisi
- Sunucu tarafı client'tan getUser()
- Veri erişimi için RLS policy'leri
- Service role key SADECE admin işlemlerinde
```

### NextAuth.js kullanan projede:
```typescript
// NextAuth session'ları
- Route handler içinde getServerSession()
- Middleware ile koruma
- Rol kontrolü mantığı
```

### Kendi auth sistemini kuranlarda:
```typescript
// JWT doğrulama
- Token'ı verify et
- Claim'leri decode edip doğrula
- Expiration kontrolü
```

## Güvenlik Kontrol Listesi

**Authentication**
- ✅ Token'lar doğrulanıyor
- ✅ Eksik/geçersiz token → 401
- ✅ Token süresi kontrol ediliyor
- ✅ Token'ın güvenli saklanması için öneri veriliyor

**Authorization**
- ✅ Rol/izin kontrolü → yetkisizse 403
- ✅ Kaynak sahipliği doğrulanıyor
- ✅ En az yetki (least privilege) ilkesi uygulanıyor
- ✅ Yetki reddedilen denemeler loglanıyor

**Girdi Doğrulama**
- ✅ Her girdi Zod'dan geçiyor
- ✅ SQL/NoSQL sorgularında parameterized query / ORM kullanılıyor (string birleştirme yok)
- ✅ Çıktıda output encoding uygulanıyor (XSS'e karşı)
- ✅ Payload boyutu sınırlanıyor

**Rate Limiting**
- ✅ Kullanıcı başına limit
- ✅ IP başına limit
- ✅ Aşımda net hata mesajı → 429
- ✅ Retry-After header'ı

**CORS**
- ✅ Belirli origin'ler whitelist'te
- ✅ Preflight istekleri ele alınıyor
- ✅ Credential'lar güvenli
- ✅ Header'lar doğru

**Hata Yönetimi**
- ✅ Stack trace asla dışarı çıkmıyor
- ✅ Dışarıya genel mesaj, detay yok
- ✅ Ayrıntılı hata sunucu tarafında loglanıyor
- ✅ Tutarlı hata formatı

**Log & İzleme**
- ✅ Giriş denemeleri loglanıyor
- ✅ Yetki hataları loglanıyor
- ✅ Şüpheli aktivite takip ediliyor
- ✅ Rate limit aşımlarının izlenmesi

## Üretilecekler

1. **Korumalı Route Handler** — endpoint'in güvenli hâli
2. **Middleware / Yardımcılar** — tekrar kullanılabilir auth fonksiyonları
3. **Tip Tanımları** — user, permission ve rol tipleri
4. **Hata Cevapları** — standart auth hataları
5. **Kullanım Örnekleri** — client tarafı entegrasyonu

## Sık Kullanılan Basit Kalıplar

**Kalıp 1: Sabit Token** (internal tool, admin paneli)
```typescript
const token = request.headers.get('authorization')
if (token !== process.env.ADMIN_TOKEN) {
  return new Response('Unauthorized', { status: 401 })
}
```

**Kalıp 2: Kullanıcı Bazlı** (son kullanıcıya açık uygulamalar)
```typescript
const user = await getCurrentUser(request)
if (!user) {
  return new Response('Unauthorized', { status: 401 })
}
```

**Kalıp 3: Rol Bazlı** (farklı kullanıcı tipleri olan uygulamalar)
```typescript
const user = await getCurrentUser(request)
if (!user || !hasRole(user, 'admin')) {
  return new Response('Forbidden', { status: 403 })
}
```

En az yetki ilkesine uyan, üretime hazır ve güvenli kod üret.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

---
description: Deno üzerinde çalışan yeni bir Supabase Edge Function oluşturur
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Sunucu kurmadan, bulutta çalışan küçük bir arka plan fonksiyonu oluşturur. Ödeme bildirimi karşılamak, zamanlanmış temizlik yapmak veya gizli API anahtarı gerektiren dış servisleri güvenle çağırmak gibi işler için idealdir.

Aşağıdaki tarife göre yeni bir Supabase Edge Function oluştur.

## Fonksiyon Tarifi

$ARGUMENTS

## Edge Function Nedir?

Edge Function'lar Deno Deploy üzerinde çalışır (Node.js DEĞİL):
- TypeScript/JavaScript desteği
- Dünya genelinde edge'de çalışır
- Supabase client'ına erişim
- HTTP ile tetiklenir
- Hızlı cold start

## Oluşturma Adımları

### 1. **Fonksiyonu başlat**

```bash
npx supabase functions new function-name
```

### 2. **Fonksiyon iskeleti**

```typescript
// supabase/functions/function-name/index.ts
import { serve } from 'https://deno.land/std@0.168.0/http/server.ts'
import { createClient } from 'https://esm.sh/@supabase/supabase-js@2'

serve(async (req: Request) => {
  try {
    // 1. İsteği parse et
    const { data } = await req.json()

    // 2. Supabase client'ı oluştur
    const supabaseClient = createClient(
      Deno.env.get('SUPABASE_URL') ?? '',
      Deno.env.get('SUPABASE_ANON_KEY') ?? '',
      {
        global: {
          headers: {
            Authorization: req.headers.get('Authorization')!
          }
        }
      }
    )

    // 3. Kullanıcıyı doğrula (gerekiyorsa)
    const {
      data: { user },
      error: authError
    } = await supabaseClient.auth.getUser()

    if (authError || !user) {
      return new Response(
        JSON.stringify({ error: 'Unauthorized' }),
        { status: 401, headers: { 'Content-Type': 'application/json' } }
      )
    }

    // 4. İş mantığı
    const result = await processData(data, user)

    // 5. Cevabı dön
    return new Response(
      JSON.stringify({ data: result }),
      {
        status: 200,
        headers: {
          'Content-Type': 'application/json',
          'Access-Control-Allow-Origin': '*'
        }
      }
    )
  } catch (error) {
    // Detayı sunucu tarafında logla, dışarıya genel mesaj dön
    console.error(error)
    return new Response(
      JSON.stringify({ error: 'Internal Server Error' }),
      {
        status: 500,
        headers: { 'Content-Type': 'application/json' }
      }
    )
  }
})
```

Not: Fonksiyon tarayıcıdan çağrılacaksa, 9. bölümdeki CORS kalıbını iskelete ekle ve CORS header'larını hata cevapları dahil TÜM cevaplarda döndür.

### 3. **Tipik Kullanım Senaryoları**

**Webhook karşılama**
```typescript
serve(async (req) => {
  const signature = req.headers.get('stripe-signature')
  // İmzayı doğrula
  // Event'i işle
  return new Response('OK', { status: 200 })
})
```

**Zamanlanmış görev** (pg_cron ile)
```typescript
serve(async () => {
  // Günlük temizlik, e-posta gönderimi vb.
  const supabase = createClient(url, serviceKey)
  await supabase.from('old_records').delete().lt('created_at', oldDate)
  return new Response('Done', { status: 200 })
})
```

**API proxy / dönüştürme**
```typescript
serve(async (req) => {
  const apiKey = Deno.env.get('THIRD_PARTY_API_KEY')
  const response = await fetch('https://api.example.com/data', {
    headers: { 'Authorization': `Bearer ${apiKey}` }
  })
  const data = await response.json()
  // Dönüştür ve geri ver
  return new Response(JSON.stringify(data), { status: 200 })
})
```

### 4. **Yerelde Test**

```bash
# Supabase'i yerelde başlat
npx supabase start

# Fonksiyonu yerelde serve et
npx supabase functions serve function-name

# curl ile dene
curl -X POST http://localhost:54321/functions/v1/function-name \
  -H "Authorization: Bearer YOUR_ANON_KEY" \
  -H "Content-Type: application/json" \
  -d '{"key":"value"}'
```

### 5. **Deploy**

```bash
# Supabase'e deploy et
npx supabase functions deploy function-name

# Secret'ları tanımla
npx supabase secrets set API_KEY=your-secret-key

# Logları izle
npx supabase functions logs function-name
```

### 6. **Frontend'den Çağırma**

```typescript
// Supabase client ile
const { data, error } = await supabase.functions.invoke('function-name', {
  body: { key: 'value' }
})

// Doğrudan fetch ile
const response = await fetch(
  `${SUPABASE_URL}/functions/v1/function-name`,
  {
    method: 'POST',
    headers: {
      'Authorization': `Bearer ${SUPABASE_ANON_KEY}`,
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({ key: 'value' })
  }
)
```

### 7. **Uyulacak İlkeler**

**Güvenlik**
- ✅ Kullanıcı kimliğini doğrula
- ✅ RLS policy'lerinden faydalan
- ✅ Tüm girdileri doğrula
- ✅ Service role key'i olabildiğince az kullan
- ✅ CORS header'larını doğru ayarla

**Performans**
- ✅ Fonksiyonları küçük ve tek amaçlı tut
- ✅ Büyük cevaplarda streaming kullan
- ✅ Mümkünse cache'le
- ✅ Timeout'lara hazırlıklı ol (üst sınır 150 sn)

**Hata Yönetimi**
- ✅ Doğru HTTP status kodları
- ✅ Tutarlı hata formatı
- ✅ Debug için hataları logla
- ✅ Hassas bilgiyi dışarı sızdırma

**Kod Düzeni**
- ✅ Dosya başına tek fonksiyon
- ✅ Ortak kodu shared klasörüne çıkar
- ✅ Tip güvenliği için TypeScript
- ✅ Deno uyumlu URL'lerden import et

### 8. **Environment Variable'lar**

```bash
# Yerelde
echo "API_KEY=secret" > supabase/functions/.env

# Üretimde
npx supabase secrets set API_KEY=secret

# Fonksiyon içinden erişim
const apiKey = Deno.env.get('API_KEY')
```

### 9. **Sık Kullanılan Kalıplar**

**CORS ele alma**
```typescript
serve(async (req) => {
  if (req.method === 'OPTIONS') {
    return new Response('ok', {
      headers: {
        'Access-Control-Allow-Origin': '*',
        'Access-Control-Allow-Methods': 'POST',
        'Access-Control-Allow-Headers': 'authorization, content-type'
      }
    })
  }
  // İsteği işle
})
```

**Veritabanı erişimi**
```typescript
// RLS ile okuma (kullanıcının token'ı geçerli)
const { data } = await supabaseClient
  .from('posts')
  .select('*')

// Admin erişimi (RLS'i atlar — dikkatli kullan)
const supabaseAdmin = createClient(url, serviceRoleKey)
const { data } = await supabaseAdmin
  .from('posts')
  .select('*')
```

Hata yönetimi, authentication ve tip güvenliği tamam olan, üretime hazır bir Edge Function üret.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

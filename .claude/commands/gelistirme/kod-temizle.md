---
description: Kodu okunabilirlik ve bakım kolaylığı için iyi pratiklere göre elden geçirir
model: claude-sonnet-4-5
---

## Bu komut ne işe yarar?
Dağınık veya zamanla hantallaşmış kodu düzenler: karmaşık yapıları sadeleştirir, tekrarları ayıklar ve kodu ileride bakımı kolay olacak şekilde yeniden yazar.

Aşağıdaki kodu okunabilirlik, bakım kolaylığı ve iyi pratikler açısından temizleyip refactor et.

## Temizlenecek Kod

$ARGUMENTS

## Temizlik Kontrol Listesi

### 1. **Giderilecek Code Smell'ler**

**İsimlendirme**
- Değişken ve fonksiyon isimleri anlamlı olsun
- İsimlendirme kuralları tutarlı olsun (camelCase, PascalCase)
- Bariz olmadıkça kısaltmadan kaçın
- Boolean isimleri is/has/can ile başlasın

**Fonksiyonlar**
- Her fonksiyon tek bir işten sorumlu olsun
- Fonksiyonları kısa tut (<50 satır)
- Parametre sayısını azalt (en fazla 3-4)
- Karmaşık mantığı ayrı fonksiyonlara çıkar
- Mümkün oldukça side effect'ten kaçın

**DRY (Kendini Tekrar Etme)**
- Tekrarlanan kodu utility fonksiyonlara taşı
- Yeniden kullanılabilir component'ler oluştur
- Tip tekrarı için TypeScript generics kullan
- Sabitleri ve konfigürasyonu tek yerde topla

**Karmaşıklık**
- İç içe if bloklarını azalt
- Karmaşık koşulları isimli fonksiyonlara çevir
- Early return kullan
- Boolean mantığını sadeleştir

**TypeScript**
- `any` tiplerini kaldır
- Eksik tip anotasyonlarını ekle
- Nesne şekilleri için interface tanımla
- Utility type'lardan yararlan (Pick, Omit, Partial)

### 2. **Uygulanacak Modern Kalıplar**

**JavaScript/TypeScript**
```typescript
// Optional chaining
const deger = obj?.prop?.nested

// Nullish coalescing
const sonuc = deger ?? varsayilan

// Destructuring
const { name, email } = user

// Template literal
const mesaj = `Merhaba, ${name}!`

// Array metodları
const filtreli = dizi.filter(x => x.active)
```

**React**
```typescript
// Custom hook'a çıkar
const useUserData = () => {
  // mantık burada
}

// Doğru TypeScript tipleri
interface Props {
  user: User
  onUpdate: (user: User) => void
}

// Prop drilling yerine composition
<Provider value={data}>
  <Component />
</Provider>
```

### 3. **Refactoring Teknikleri**

**Extract Function**
```typescript
// Önce
const isle = () => {
  // 50 satırlık kod
}

// Sonra
const dogrula = () => { /* ... */ }
const donustur = () => { /* ... */ }
const kaydet = () => { /* ... */ }

const isle = () => {
  dogrula()
  const veri = donustur()
  kaydet(veri)
}
```

**Koşulu Polymorphism ile Değiştir**
```typescript
// Önce
if (tur === 'A') return isleA()
if (tur === 'B') return isleB()

// Sonra
const isleyiciler = {
  A: isleA,
  B: isleB
}
return isleyiciler[tur]()
```

**Parameter Object Kullan**
```typescript
// Önce
function olustur(name, email, age, address)

// Sonra
interface UserData {
  name: string
  email: string
  age: number
  address: string
}
function olustur(userData: UserData)
```

### 4. **Rutin Temizlik İşleri**

**Ölü Kodu Sil**
- Kullanılmayan import'lar
- Erişilemeyen (unreachable) kod
- Yorum satırına alınmış eski kod
- Kullanılmayan değişkenler

**Hata Yönetimini Güçlendir**
```typescript
// Önce
try { birSeyYap() } catch (e) { console.log(e) }

// Sonra
try {
  birSeyYap()
} catch (error) {
  if (error instanceof ValidationError) {
    // Validasyon hatasını ele al
  } else {
    logger.error('Beklenmeyen hata', { error })
    throw error
  }
}
```

**Tutarlı Biçimlendirme**
- Düzgün girinti
- Tutarlı tırnak kullanımı
- Satır uzunluğu (<100 karakter)
- Düzenli import sıralaması

**Daha İyi Yorumlar**
- Bariz olanı anlatan yorumları sil
- "Ne yapıldığını" değil "neden yapıldığını" yaz
- Karmaşık mantığı belgele
- Eskimiş yorumları güncelle

### 5. **Next.js / React Özelinde**

**Server ve Client Component Ayrımı**
```typescript
// State'i client component'e taşı
'use client'
function Etkilesimli() {
  const [state, setState] = useState()
}

// Veri çekmeyi server component'te tut
async function Page() {
  const data = await fetchData()
}
```

**Doğru Veri Çekme**
```typescript
// Client tarafında SWR / React Query
const { data } = useSWR('/api/user')

// Server component'te doğrudan fetch
const data = await fetch('/api/user').then(r => r.json())
```

## Çıktı Formatı

1. **Bulunan Sorunlar** — code smell'lerin ve problemlerin listesi
2. **Temizlenmiş Kod** — refactor edilmiş sürüm
3. **Açıklamalar** — ne değişti, neden değişti
4. **Önce/Sonra Karşılaştırması** — faydalıysa yan yana göster
5. **İleri İyileştirmeler** — opsiyonel öneriler

Over-engineering yapmadan, kodu gerçekten daha bakımı kolay hale getiren pratik iyileştirmelere odaklan. Temiz kod ile pragmatizm arasındaki dengeyi koru.

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

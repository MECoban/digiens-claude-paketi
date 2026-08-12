# Paketteki MCP Sunucuları

Bu paket, Claude Code'un yeteneklerini genişleten 3 hazır MCP sunucusuyla gelir.

**MCP ne demek?** Claude'a yeni "eller" takan bir eklenti standardı. Normalde Claude sadece kodunuzu görür; MCP sunucularıyla tarayıcıyı kullanabilir, veritabanınıza bakabilir, güncel dokümantasyona ulaşabilir.

## Dahil Olan Sunucular

### 1. **Context7** (`@upstash/context7-mcp`)
**Ne yapar?** Kullandığınız herhangi bir kütüphanenin güncel ve sürüme özel dokümantasyonunu Claude'un önüne getirir.

**Nasıl kullanılır?** Güncel dokümana ihtiyaç duyduğunuzda prompt'a "use context7" eklemeniz yeterli.

**Faydası:**
- Doküman her zaman güncel
- Sürüme özel bilgi (eski API önerilerine takılmazsınız)
- Binlerce kütüphaneyle çalışır
- Elle arama derdi biter

**Girişimci notu — ne zaman lazım?** Claude size eski bir kütüphane kullanımı önerdiğinde ya da "bu yeni sürümde nasıl yapılıyordu?" dediğiniz her an. Yeni framework sürümleriyle çalışırken saatlerce yanlış dokümanla boğuşmayı engeller.

### 2. **Playwright** (`@playwright/mcp`)
**Ne yapar?** Claude'a tarayıcı kullandırır: siteleri gezer, tıklar, form doldurur, ekran görüntüsü alır.

**Yetenekleri:**
- Web sitelerinde gezinme
- Ekran görüntüsü alma
- Sayfa elemanlarıyla etkileşim
- Test kodu üretme
- Accessibility tree'ye erişim

**Kullanım alanları:**
- E2E (uçtan uca) test
- Web scraping
- Tarayıcı otomasyonu
- Görsel test

**Girişimci notu — ne zaman lazım?** "Sitem gerçekten çalışıyor mu?" sorusunun cevabını Claude'un kendi gözüyle görmesini istediğinizde. Örneğin yeni landing page'inizin kayıt formunu Claude'un baştan sona tıklayarak test etmesi için. Ürünü müşteriye açmadan önceki son kontrol turlarında çok değerli.

### 3. **Supabase** (`@supabase/mcp-server-supabase`)
**Ne yapar?** Claude'u doğrudan Supabase veritabanınıza bağlar.

**Yetenekleri:**
- Veritabanı sorgulama
- Tablo yönetimi
- SQL çalıştırma
- Authentication işlemleri
- Storage ile çalışma

**Kullanım alanları:**
- Veritabanı yönetimi
- Şema keşfi
- Veri sorguları
- Admin işlemleri

**Girişimci notu — ne zaman lazım?** "Kaç kullanıcım var?", "dün kaç sipariş geldi?" gibi soruları SQL bilmeden Claude'a sorabilmek için. Ayrıca Claude kod yazarken tablolarınızın gerçek yapısını gördüğünden, hayalî kolonlara kod yazma hatası ortadan kalkar. Ürününüz Supabase üzerindeyse bu sunucu vazgeçilmezdir.

## Pakete Dahil Olmayanlar

Sık sorulan bazı servisler ilk sürüme bilinçli olarak eklenmedi:

- **chrome-devtools** — tarayıcı ihtiyacını şimdilik Playwright karşılıyor
- **stripe** — ödeme altyapısı hassas bir alan; resmî sunucusunu kendiniz doğrulayıp eklemeniz daha güvenli
- **vercel** — deploy işlemleri için şimdilik CLI yeterli

MCP ekosistemi hızlı gelişiyor; bu servislerin güncel resmî sunucularını eklemeden önce ilgili firmanın kendi dokümantasyonundan doğrulayın.

## MCP Sunucularını Kullanmak

Paketi kurduktan sonra:

1. **Otomatik başlarlar** — paketi kullandığınız anda MCP sunucuları devreye girer
2. **Yeniden başlatma gerekir** — paket kurulumundan sonra Claude Code'u bir kez kapatıp açın
3. **Araç listesinde görünürler** — MCP araçları Claude'un kullanılabilir araçları arasına eklenir

## Yeni MCP Sunucusu Eklemek

Kendi sunucularınızı yerel `.claude/.mcp.json` dosyasına ekleyebilirsiniz:

```json
{
  "server-name": {
    "command": "npx",
    "args": ["-y", "package-name"],
    "env": {
      "API_KEY": "your-key"
    }
  }
}
```

## Sorun Giderme

**MCP sunucuları yüklenmiyor mu?**
1. Claude Code'u yeniden başlatın
2. npm/npx kurulu mu kontrol edin
3. İnternet bağlantınızı kontrol edin (sunucular ilk kullanımda indirilir)

**Yavaşlık mı var?**
- MCP sunucuları ihtiyaç anında (on-demand) çalışır
- İlk kullanım yavaş olabilir (paket indiriliyor)
- Sonraki kullanımlar hızlıdır

## Daha Fazlası

- Resmî MCP dokümantasyonu: https://modelcontextprotocol.io
- Claude Code MCP rehberi: https://docs.claude.com/en/docs/claude-code/mcp
- MCP sunucu dizini: https://mcpcat.io

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

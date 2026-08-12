# Yayınlama Rehberi: Claude Code Paketini GitHub'da Paylaşmak

Bu rehber, paketi GitHub'a çıkarıp başkalarının tek komutla kurabileceği hâle getirmenin tüm adımlarını anlatır.

> Not: Aşağıdaki `SAHIBI/REPO-ADI` ifadesi bir yer tutucudur — yayına çıkarken kendi GitHub kullanıcı adın ve repo adınla değiştir.

## Ön Koşullar

- [ ] GitHub hesabı
- [ ] Yerelde kurulu git
- [ ] Repo adına karar verilmiş olması
- [ ] Tüm konfigürasyon dosyalarının güncel olması

## Adım 1: GitHub Reposunu Oluştur

### 1.1 GitHub'da yeni repo aç

1. https://github.com/new adresine git
2. Bilgileri doldur:
   - **Repository name**: `REPO-ADI`
   - **Description**: Paketin kısa tanıtımı (örn. "Web geliştirme için Türkçe slash komutları ve uzman AI agent'ları içeren Claude Code paketi")
   - **Visibility**: Public (başkaları kurabilsin diye)
   - **Initialize**: ❌ README, .gitignore veya lisans EKLEME — bunlar yerel repoda zaten var
3. "Create repository" butonuna bas

### 1.2 Yerel repoyu push'la

GitHub reposu oluştuktan sonra:

```bash
cd ~/Projects/REPO-ADI

# GitHub remote'unu ekle
git remote add origin https://github.com/SAHIBI/REPO-ADI.git

# Kodu gönder
git push -u origin main
```

Kimlik doğrulama sorunu yaşarsan:
- Şifre yerine Personal Access Token kullan
- Ya da SSH anahtarı kur (önerilen): https://docs.github.com/en/authentication/connecting-to-github-with-ssh

## Adım 2: Kurulumun Çalıştığını Doğrula

Paketin gerçekten kurulabildiğini kendin test et:

```bash
# Kendi GitHub reposundan kur
/plugin install SAHIBI/REPO-ADI

# Komutların geldiğini kontrol et
/kod-acikla
/ozellik-plani

# Agent'lar bağlama göre kendiliğinden devreye girer, ayrıca komut gerekmez
```

Sıfırdan tekrar denemek için:
```bash
/plugin uninstall REPO-ADI
```

## Adım 3: Paketi Duyur

README dosyanda kurulum komutu hazır durursa kullanıcılar kopyala-yapıştır ile kurabilir.

### Seçenek A: Doğrudan kurulum komutunu paylaş

```bash
/plugin install SAHIBI/REPO-ADI
```

### Seçenek B: Topluluk marketplace'lerine gönder

#### Claude Code Plugins Marketplace
1. https://claudecodemarketplace.com/ adresine git
2. Gönderim kurallarını takip et
3. Paket bilgilerini paylaş

#### CC Plugins Küratörlü Marketplace
1. https://github.com/ccplugins/marketplace adresine git
2. Repoyu fork'la
3. Paketini `marketplace.json` dosyasına ekle
4. Şu formatta bir Pull Request aç:

```json
{
  "name": "REPO-ADI",
  "source": "SAHIBI/REPO-ADI",
  "description": "Modern web geliştirme için Türkçe slash komutları ve uzman AI agent'ları içeren Claude Code paketi",
  "version": "1.0.0",
  "author": "SAHIBI",
  "tags": ["productivity", "nextjs", "supabase", "typescript", "react", "development", "turkish"]
}
```

#### Claude Code Plugins Plus
1. https://github.com/jeremylongshore/claude-code-plugins-plus adresine git
2. Katkı kurallarını takip et
3. Paket bilgilerini gönder

### Seçenek C: Sosyal medyada duyur

Örnek paylaşım:

```
🚀 Claude Code kurulumumu paket olarak yayınladım!

Verimli web geliştirme için 14 slash komutu + 11 uzman AI agent — Türkçe.

Kurulum:
/plugin install SAHIBI/REPO-ADI

Öne çıkanlar:
✅ API iskeleti (/yeni-api)
✅ Kod optimizasyonu (/kod-hizlandir)
✅ Özellik planlama (/ozellik-plani)
✅ Teknoloji araştırma agent'ı
✅ Mimari agent'ları
✅ Güvenlik & performans agent'ları

Next.js, React, TypeScript ve Supabase projeleri için birebir!

GitHub: https://github.com/SAHIBI/REPO-ADI
```

## Adım 4: Paketi Canlı Tut

### Güncelleme akışı

Yereldeki kurulumunda değişiklik yaptığında:

```bash
cd ~/Projects/REPO-ADI

# Komut/agent değişikliklerini yap, sonra:

git add .
git commit -m "feat: add /yeni-komut command"

# plugin.json içindeki versiyonu yükselt
# örn. 1.0.0 -> 1.1.0

git add .claude-plugin/plugin.json
git commit -m "chore: bump version to 1.1.0"

git push
```

Kullanıcılar en yeni sürüme şöyle geçer:
```bash
/plugin update REPO-ADI
```

### Versiyonlama kuralları

- **1.0.x** — bug fix'ler ve ufak rötuşlar
- **1.x.0** — yeni komut veya agent eklendi
- **x.0.0** — büyük yeniden yapılanma ya da breaking change

## Sorun Giderme

### Paket kurulmuyor

Şunları kontrol et:
- Repo GitHub'da public mi?
- `.claude-plugin/plugin.json` repo kökünde duruyor mu?
- JSON dosyaları geçerli mi? (sonda virgül kalmış olabilir, tırnaklar bozuk olabilir)

### Komutlar görünmüyor

Şunları kontrol et:
- `plugin.json` içindeki komut path'leri gerçek dosya konumlarıyla eşleşiyor mu?
- Komut dosyalarının uzantısı `.md` mi?
- Komut dosyaları boş mu kalmış?

### Agent'lar devreye girmiyor

Şunları kontrol et:
- `plugin.json` içindeki agent path'leri doğru mu?
- Agent dosyalarının frontmatter'ında `name` ve `description` var mı?
- Agent'lar komutla değil, bağlama göre aktive olur — bu normal davranış

## İleri Seviye: GitHub Release Oluşturma

Önemli sürümler için release çıkar:

1. Repoya git: https://github.com/SAHIBI/REPO-ADI
2. "Releases" → "Create a new release"
3. Tag: `v1.0.0`
4. Başlık: `v1.0.0 - İlk Sürüm`
5. Açıklama: özellik/değişiklik listesi
6. "Publish release" butonuna bas

Kullanıcılar belirli bir sürümü kurabilir:
```bash
/plugin install SAHIBI/REPO-ADI@v1.0.0
```

## Başarıyı Ölç

Paketin nasıl gittiğini şuradan izle:
- ⭐ GitHub yıldızları
- 👁️ İzleyenler (watchers)
- 🍴 Fork sayısı
- 💬 Issue ve tartışmalar
- 📊 Clone/indirme sayıları (GitHub Insights)

## Yardım Kaynakları

Takılırsan:
- Claude Code dokümanları: https://docs.claude.com/en/docs/claude-code/plugin-marketplaces
- GitHub Issues: https://github.com/anthropics/claude-code/issues
- Topluluk: GitHub'da diğer Claude Code paketlerini incele

---

**Tebrikler!** Yayına çıktığı andan itibaren paketin tüm Claude Code topluluğunun kullanımına ve öğrenmesine açık olacak. 🎉

<!-- Uyarlama temeli: github.com/edmund-io/edmunds-claude-code -->

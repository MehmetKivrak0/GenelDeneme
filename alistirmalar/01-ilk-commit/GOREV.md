# 01. Alıştırma: İlk commit ve ilk pull request

**Amaç:** Repoyu bilgisayarına indirmek, kendi branch'ini açmak, bir dosya ekleyip commit
etmek, push etmek ve pull request açmak.

**Süre:** 20-30 dakika

## Adımlar

### 1. Repoyu bilgisayarına indir

```bash
git clone https://github.com/MehmetKivrak0/GenelDeneme.git
cd GenelDeneme
```

Bunu sadece bir kez yapacaksın. Sonraki alıştırmalarda aynı klasörde çalışmaya devam et.

### 2. Kendini tanıt

Git'e commit'lerin kimin adına atılacağını söylemen gerekiyor:

```bash
git config user.name "Ad Soyad"
git config user.email "github-hesabindaki-mail@ornek.com"
```

Buraya GitHub hesabına kayıtlı mail adresini yaz. Yoksa commit'lerin GitHub profilinde
sana bağlanmaz.

### 3. Branch aç

```bash
git checkout main
git pull
git checkout -b alistirma-01/ad-soyad
```

`git pull` komutunu atlama. Branch açmadan önce main'in güncel halini almak, ileride
gereksiz çakışmalardan kurtarır.

### 4. Kendi dosyanı ekle

`katilimcilar/` klasörünün içine `ad-soyad.md` adında bir dosya oluştur. Türkçe karakter
ve boşluk kullanma, `ayse-yilmaz.md` gibi olsun.

İçeriği için `katilimcilar/ORNEK-eren-ata.md` dosyasına bak, aynı şablonu doldur.

### 5. Commit et

```bash
git status
git add katilimcilar/ad-soyad.md
git commit -m "01. alistirma: ad soyad katilimci dosyasi eklendi"
```

`git add .` yerine dosya adını tek tek yazmayı dene. Neyi commit'e dahil ettiğini bilerek
çalışmak, sonradan "bu dosya buraya nasıl girdi" sorusunu yaşamamanı sağlar.

### 6. Push et

```bash
git push -u origin alistirma-01/ad-soyad
```

### 7. Pull request aç

GitHub'da repoya gir, çıkan "Compare & pull request" butonuna bas. Başlığı ve açıklamayı
doldur, sonra sağdaki "Reviewers" kısmından bir arkadaşını review'a ekle.

Açıklamada şunlar olsun:
- Ne yaptın (bir cümle yeterli)
- Takıldığın bir yer olduysa nerede takıldın

### 8. Review'ı bekle

Onay gelene kadar merge edemezsin, bu normal. Bu arada bir arkadaşının pull request'ine
gir ve sen de ona review bırak. Review yazarken "olmuş" demek yerine somut konuş:
dosya adı şablona uymuyorsa onu söyle, eksik alan varsa onu göster.

## Bittiğinde kontrol et

- [ ] Dosyan `katilimcilar/` klasörünün içinde
- [ ] Dosya adında Türkçe karakter, boşluk ve büyük harf yok
- [ ] Pull request'inde sadece 1 dosya değişmiş görünüyor
- [ ] En az bir kişiye review isteği gönderdin
- [ ] En az bir kişinin pull request'ine review bıraktın

## Sık karşılaşılan hatalar

**`fatal: not a git repository`**
Yanlış klasördesin. `cd GenelDeneme` yapmayı unutmuş olabilirsin.

**Push ederken `Permission denied` veya kimlik doğrulama hatası**
Repoya collaborator olarak eklenmemiş olabilirsin, yetkilinden ekletmen gerekiyor.
Şifre soran ekranda GitHub şifreni yazma, o yöntem kapalı. Kolay yolu
[GitHub CLI](https://cli.github.com) kurup `gh auth login` demek.

**Pull request'te olması gerekenden fazla dosya değişmiş görünüyor**
Büyük ihtimalle branch açmadan önce `git pull` yapmadın ya da yanlış branch'ten dallandın.
`git log --oneline --graph --all` ile nereden dallandığına bak.

# 03. Alıştırma: Çakışma (conflict) çıkarma ve çözme

**Amaç:** Bilerek bir merge conflict oluşturmak, git'in ne dediğini okumak ve çakışmayı
elle çözmek.

**Süre:** 30-40 dakika

Bu klasördeki `takim-listesi.md` dosyası bu iş için hazırlandı. İçinde tek satırlık bir
alan var ve iki branch'te de tam olarak o satırı değiştireceksin. Git iki değişikliğin
hangisinin doğru olduğunu bilemeyeceği için kararı sana bırakacak.

## Adımlar

### 1. Güncel main'den başla

```bash
git checkout main
git pull
```

### 2. Birinci branch

```bash
git checkout -b alistirma-03/ad-soyad-a
```

`takim-listesi.md` dosyasını aç. Şu satırı bul:

```
- Sprint sorumlusu: BELIRLENECEK
```

`BELIRLENECEK` yerine kendi adını yaz. Sonra:

```bash
git add takim-listesi.md
git commit -m "03. alistirma: sprint sorumlusu A dalinda belirlendi"
```

### 3. İkinci branch

Yine main'den dallanıyorsun:

```bash
git checkout main
git checkout -b alistirma-03/ad-soyad-b
```

Aynı dosyayı aç, **aynı satırı** bul ve bu sefer `BELIRLENECEK` yerine bir arkadaşının
adını yaz:

```bash
git add takim-listesi.md
git commit -m "03. alistirma: sprint sorumlusu B dalinda belirlendi"
```

### 4. Çakışmayı çıkar

```bash
git checkout alistirma-03/ad-soyad-a
git merge alistirma-03/ad-soyad-b
```

Şuna benzer bir çıktı alacaksın:

```
Auto-merging alistirmalar/03-conflict-cozme/takim-listesi.md
CONFLICT (content): Merge conflict in alistirmalar/03-conflict-cozme/takim-listesi.md
Automatic merge failed; fix conflicts and then commit the result.
```

Panikleme, bu bir hata değil. Git sana "bu satırda ne yapacağıma karar veremedim, sen
karar ver" diyor. Şu an merge yarım kalmış durumda.

### 5. Nerede olduğunu gör

```bash
git status
```

`Unmerged paths` başlığının altında çakışan dosyayı göreceksin. Hangi komutları
kullanabileceğini de git sana burada söylüyor, okumadan geçme.

### 6. Dosyayı aç ve bak

Dosyada şöyle bir şey duruyor olacak:

```
<<<<<<< HEAD
- Sprint sorumlusu: Ayşe Yılmaz
=======
- Sprint sorumlusu: Mehmet Kıvrak
>>>>>>> alistirma-03/ad-soyad-b
```

Okuma şekli:

- `<<<<<<< HEAD` ile `=======` arası: **şu an bulunduğun branch'teki** hali
- `=======` ile `>>>>>>>` arası: **merge etmeye çalıştığın branch'teki** hali
- `>>>>>>>` satırının sonundaki isim, değişikliğin geldiği branch

### 7. Çöz

Çözmek demek, dosyayı olması gerektiği gibi elle yazmak demek. `<<<<<<<`, `=======` ve
`>>>>>>>` satırlarının **hepsini sil**, geriye tek bir doğru satır kalsın:

```
- Sprint sorumlusu: Ayşe Yılmaz
```

İstersen iki ismi de bırakabilirsin, doğrusu ne ise onu yaz. Önemli olan işaretçilerden
hiçbirinin dosyada kalmaması. Bu işaretçilerin unutulup commit edilmesi en sık yapılan
hatalardan biri.

### 8. Çözdüğünü git'e söyle

```bash
git add takim-listesi.md
git status
git commit
```

`git add` burada "bu dosyadaki çakışmayı çözdüm" anlamına geliyor. `git commit` merge'ü
tamamlar, hazır mesajı kabul edip çıkabilirsin.

### 9. Sonuca bak

```bash
git log --oneline --graph --all
```

İki dalın birleştiğini ve bu sefer birleşme noktasının senin çözdüğün merge commit'i
olduğunu göreceksin.

### 10. Push et ve pull request aç

```bash
git push -u origin alistirma-03/ad-soyad-a
```

Pull request açıklamasına şunu yaz: çakışma hangi satırda çıktı, neden çıktı ve hangi
tarafı seçtin.

## Bittiğinde kontrol et

- [ ] Merge sırasında CONFLICT mesajını gördün
- [ ] `git status` çıktısında `Unmerged paths` satırını okudun
- [ ] Dosyada `<<<<<<<`, `=======`, `>>>>>>>` işaretlerinden hiçbiri kalmadı
- [ ] Merge commit'i attın ve pull request'ini açtın

## Bonus: yarım kalan merge'den çıkmak

Bir merge'e başlayıp vazgeçmek istersen, her şeyi merge öncesindeki haline geri alan komut:

```bash
git merge --abort
```

Bunu 4. adımı tekrar edip deneyebilirsin. Merge'i başlat, dosyaya bak, sonra `--abort`
ile geri dön ve `git status` ile tertemiz olduğunu gör. Bu komutu bilmek, çakışma
gördüğünde klasörü silip repoyu baştan indirmekten kurtarır.

## Çakışma neden çıkar, nasıl azaltılır

Çakışma, iki kişinin aynı dosyanın aynı satırlarını farklı şekilde değiştirmesinden çıkar.
Git'in hatası değil, aynı anda çalışmanın doğal sonucu. Tamamen kaçınılamaz ama azaltılır:

- Branch açmadan önce ve çalışırken sık sık `git checkout main && git pull` yap
- Branch'lerini günlerce açık tutma, küçük parçalar halinde merge et
- Aynı dosya üzerinde çalışan varsa haberleşin, kimin nereye dokunacağını bölüşün

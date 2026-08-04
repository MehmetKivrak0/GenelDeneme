# 02. Alıştırma: Branch açma ve merge etme

**Amaç:** Aynı anda iki ayrı branch'te çalışmak, ikisini birleştirmek ve branch'lerin
birbirine göre nerede durduğunu okuyabilmek.

**Süre:** 30-40 dakika

Bu alıştırmada iki farklı kişiymişsin gibi davranacaksın. İki branch açıp aynı dosyanın
**farklı bölümlerini** düzenleyeceksin. Farklı bölüm olduğu için git bu ikisini kendi
kendine birleştirebilecek. Aynı satıra dokunduğunda ne olduğunu 03. alıştırmada göreceğiz.

## Adımlar

### 1. Güncel main'den başla

```bash
git checkout main
git pull
```

### 2. Birinci branch: arayüz notu

```bash
git checkout -b alistirma-02/ad-soyad-arayuz
```

`proje-notlari.md` dosyasını aç, **Arayüz** başlığının altındaki listeye kendi adınla bir
madde ekle. Sonra:

```bash
git add proje-notlari.md
git commit -m "02. alistirma: arayuz notu eklendi"
```

### 3. İkinci branch: test notu

Şimdi başa dönüyoruz. Dikkat et, bu branch'i `alistirma-02/ad-soyad-arayuz` üzerinden
değil, **main üzerinden** açıyorsun:

```bash
git checkout main
git checkout -b alistirma-02/ad-soyad-test
```

Aynı dosyayı aç, bu sefer **Test** başlığının altındaki listeye bir madde ekle:

```bash
git add proje-notlari.md
git commit -m "02. alistirma: test notu eklendi"
```

### 4. Durumu gör

```bash
git log --oneline --graph --all
```

Çıktıda iki dalın main'den ayrılıp yan yana ilerlediğini göreceksin. Bu görüntüyü
anlamadan devam etme, git'in geri kalanı bu resmin üzerine kuruluyor.

### 5. İkisini birleştir

Arayüz branch'ine geçip test branch'ini onun içine merge edeceksin:

```bash
git checkout alistirma-02/ad-soyad-arayuz
git merge alistirma-02/ad-soyad-test
```

Git bir merge commit oluşturacak ve mesajını yazman için editör açabilir. Varsayılan mesaj
yeterli, kaydedip çık. (Vim açıldıysa: `:wq` yazıp Enter.)

Şimdi `proje-notlari.md` dosyasına bak. İki maddenin de içinde olduğunu göreceksin.
Sen dosyayı elle birleştirmedin, bunu git yaptı, çünkü iki değişiklik dosyanın farklı
yerlerindeydi.

### 6. Tekrar log'a bak

```bash
git log --oneline --graph --all
```

Ayrılan iki dalın tekrar tek noktada birleştiğini göreceksin. Bu birleşme noktası merge
commit'i.

### 7. Push et ve pull request aç

```bash
git push -u origin alistirma-02/ad-soyad-arayuz
```

Pull request'in açıklamasına `git log --oneline --graph --all` çıktısını yapıştır ve
merge'ün neden çakışmadan geçtiğini bir cümleyle yaz.

### 8. Pull request merge edildikten sonra temizlik

```bash
git checkout main
git pull
git branch -d alistirma-02/ad-soyad-arayuz
git branch -d alistirma-02/ad-soyad-test
```

`-d` küçük harfle, sadece merge edilmiş branch'leri siler. Eğer git silmene izin vermezse
o branch'teki değişiklik henüz hiçbir yere girmemiş demektir, önce ona bak. `-D` ile
zorlamak, o çalışmayı çöpe atmak anlamına gelir.

## Bittiğinde kontrol et

- [ ] İki ayrı branch açtın ve ikincisini main'den dallandırdın
- [ ] `git log --oneline --graph --all` çıktısını okuyup ne anlattığını anlatabiliyorsun
- [ ] Merge sonrası dosyada iki madde de duruyor
- [ ] Pull request'in merge edildi ve iki local branch'i de sildin

## Not: fast-forward nedir

Eğer bir branch açıp commit atsaydın ve bu sırada main hiç değişmeseydi, merge sırasında
git yeni bir commit oluşturmaz, sadece main etiketini ileri kaydırırdı. Buna fast-forward
denir. Bu alıştırmada iki dal da main'den ayrıldığı ve ikisinde de yeni commit olduğu için
fast-forward mümkün değildi, git merge commit'i oluşturmak zorundaydı.

Şunu deneyip farkı görebilirsin:

```bash
git log --oneline --graph
git merge --no-ff   # fast-forward mümkün olsa bile merge commit'i oluşturmaya zorlar
```

# Başlarken

Bu klasördeki alıştırmalar sırayla yapılmak üzere hazırlandı. Her klasörde bir `GOREV.md`
dosyası var, ne yapacağın orada adım adım yazıyor.

Sıra:

1. `01-ilk-commit` - repoyu bilgisayarına indirme, ilk commit, ilk pull request
2. `02-branch-merge` - branch açma, paralel çalışma, merge etme
3. `03-conflict-cozme` - bilerek çakışma çıkarma ve çözme

Görevlerdeki `git add dosya-adi.md` gibi komutlar, o alıştırmanın klasöründeyken
çalıştırıldığını varsayıyor. Terminalde önce ilgili klasöre gir:

```bash
cd alistirmalar/02-branch-merge
```

Nerede olduğundan emin değilsen `git status` sana değişen dosyaların repo kökünden
itibaren tam yolunu gösterir.

## Kurallar

- `main` branch'ine doğrudan push yapılmıyor. Her değişiklik kendi branch'inde açılır ve
  pull request ile main'e girer. Pull request en az bir kişi onaylamadan merge edilemez.
- Branch isimlerinde şu formatı kullan: `alistirma-01/ad-soyad`
  Örnek: `alistirma-01/ayse-yilmaz`
- Commit mesajlarını Türkçe ve tek satır yaz, ne yaptığını anlatsın.
  İyi: `01. alistirma: katilimci dosyasi eklendi`
  Kötü: `guncelleme`, `asd`, `deneme 3`
- Başkasının dosyasını silme veya değiştirme. Sadece kendi eklediğin dosyaya dokun.
  (03. alıştırma bunun tek istisnası, orada zaten çakışma çıkarmanı istiyoruz.)

## Her alıştırmada tekrar edeceğin temel akış

```bash
git checkout main
git pull
git checkout -b alistirma-01/ad-soyad
# dosyalarda değişiklik yap
git add .
git commit -m "aciklayici bir mesaj"
git push -u origin alistirma-01/ad-soyad
```

Push'tan sonra GitHub'da repoya girdiğinde "Compare & pull request" butonu çıkacak.
Oradan pull request'i aç, açıklama kısmını doldur ve bir arkadaşından review iste.

## Takıldığında

Bir şeyi bozmaktan korkma. Git'te push edilmemiş hiçbir hata kalıcı değil, push edilmiş
olanların da geri alma yolu var. Takılırsan repoda issue aç, sorunu ve aldığın hatayı
olduğu gibi yaz. Hata mesajını kopyalayıp yapıştırmak, "çalışmıyor" demekten çok daha
hızlı sonuç verir.

Sık kullanacağın iki komut:

```bash
git status
git log --oneline --graph --all
```

`git status` sana o an nerede olduğunu, `git log --oneline --graph --all` ise branch'lerin
birbirine göre nerede durduğunu gösterir. Kafan karıştığında önce bu ikisine bak.

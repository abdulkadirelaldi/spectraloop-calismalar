# Spectraloop Çalışmalar

Spectraloop takımının ortak çalışma alanı. Her çalışma kendi klasöründe tutulur, her üye o çalışmanın içinde **kendi adıyla bir klasör** açar ve yaptıklarını oraya yükler.

## Çalışmalar

| # | Çalışma | Tarih | Klasör |
|---|---------|-------|--------|
| 01 | STM32 ile DS18B20 sıcaklık sensöründen veri okuma | 16.10.2026 | [01-ds18b20-stm32](01-ds18b20-stm32) |

## Klasör yapısı

```
spectraloop-calismalar/
├── 01-ds18b20-stm32/
│   ├── README.md          ← çalışmanın tanımı
│   ├── abdulkadir-elaldi/ ← herkes kendi klasörü
│   ├── ahmet-yilmaz/
│   └── ...
└── 02-sonraki-calisma/
    └── ...
```

## Kurallar

1. Klasör adı: `ad-soyad` — küçük harf, Türkçe karakter yok, boşluk yerine `-` (örn. `abdulkadir-elaldi`).
2. **Sadece kendi klasörüne** dosya ekle/değiştir. Başkasının klasörüne dokunma.
3. Kendi klasörüne kısa bir `README.md` koy: ne yaptın, hangi kart/pinler, nasıl çalıştırılır, çıktı/ekran görüntüsü.
4. Derleme çıktılarını (`Debug/`, `Release/`, `build/`) yükleme — `.gitignore` zaten engelliyor.
5. Yeni çalışma klasörü sadece repo sahibi tarafından açılır: `NN-konu-adi` formatında.

## Nasıl yüklerim?

### Git ile
```bash
git clone https://github.com/abdulkadirelaldi/spectraloop-calismalar.git
cd spectraloop-calismalar
git pull                                  # her zaman önce güncelle
mkdir -p 01-ds18b20-stm32/ad-soyad
# ... dosyalarını bu klasöre kopyala ...
git add 01-ds18b20-stm32/ad-soyad
git commit -m "01-ds18b20: ad-soyad çalışması"
git push
```
`push` reddedilirse: `git pull --rebase` yapıp tekrar `git push`.

### Tarayıcıdan (git bilmeyenler için)
Çalışma klasörüne gir → **Add file → Upload files** → dosyaları sürükle. Dosya adının başına `ad-soyad/` yazarak kendi klasörünü oluşturabilirsin.

> Yazma yetkisi için repo sahibinden collaborator daveti iste.

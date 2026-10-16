# 01 — STM32 ile DS18B20 Okuma

**Tarih:** 16.10.2026

## Hedef
STM32 ile DS18B20 dijital sıcaklık sensöründen 1-Wire üzerinden sıcaklık okumak ve sonucu (UART / debugger / ekran) göstermek.

## Donanım notları
- DS18B20 pinleri: GND, DQ (data), VDD (3.3 V)
- DQ hattına VDD'ye **4.7 kΩ pull-up** şart
- Data pini GPIO **open-drain output** olarak ayarlanabilir
- 1-Wire zamanlamaları için µs gecikme gerekir (örn. TIM ile `delay_us`)

## Temel akış
1. Reset + presence pulse
2. `0xCC` Skip ROM → `0x44` Convert T
3. Dönüşümü bekle (12-bit için ~750 ms)
4. Reset → `0xCC` Skip ROM → `0xBE` Read Scratchpad
5. İlk 2 bayt: `raw = (MSB << 8) | LSB`, `°C = raw / 16.0`

## Teslim
Kendi klasörünü aç (`ad-soyad/`) ve şunları koy:
- Kaynak kod (`Core/`, `.ioc` dosyası veya proje klasörü)
- `README.md`: kullandığın kart, pin, sonuç (ekran görüntüsü / log)

## Katılımcılar
<!-- Klasörünü açınca adını ekleyebilirsin -->

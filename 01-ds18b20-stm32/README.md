# 01 — STM32 ile DS18B20 Okuma

**Tarih:** 16.10.2026

## Hedef
STM32 ile DS18B20 dijital sıcaklık sensöründen 1-Wire üzerinden sıcaklık okumak ve sonucu (UART / debugger / ekran) göstermek.

## Kart: NUCLEO-F411RE — Bağlantı

```
        DS18B20 (düz yüz sana bakıyor, bacaklar aşağıda)
           ┌───────┐
           │       │
           └┬──┬──┬┘
            1  2  3
           GND DQ VDD
            │  │   │
            │  │   ├──────────────┬──── 3V3   (CN6)
            │  │  ┌┴┐             │
            │  │  │ │ R1 4.7 kΩ   │
            │  │  └┬┘ (pull-up)   │
            │  ├───┴──────────────┼──── PA1   (CN8, "A1" yazan pin)
            │  │                  │
            └──┴──────────────────┴──── GND   (CN6)
```

| DS18B20 bacağı | Nucleo pini | Header | Prob kablo rengi |
|---|---|---|---|
| 1 · GND | GND | CN6 | Siyah |
| 2 · DQ (veri) | **PA1** | CN8 → `A1` | Sarı (bazen beyaz/mavi) |
| 3 · VDD | **3V3** (5V değil) | CN6 | Kırmızı |
| R1 4.7 kΩ | DQ ↔ 3V3 arası | breadboard | 3 pinli modülde genelde hazır takılı |

### CubeMX
- **PA1:** GPIO_Output, **Open Drain**, No pull, High speed, label `DS18B20`
- **TIM2:** Internal clock, Prescaler `100-1` (SYSCLK 100 MHz → 1 µs/tick), Period `0xFFFFFFFF`
- **USART2:** PA2/PA3, 115200 8N1 → ST-LINK sanal COM portu (ekstra kablo yok)
- PA2/PA3 (UART), PA5 (LED), PA13/PA14 (debug) pinlerini 1-Wire için **kullanma**

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

<img width="2816" height="1536" alt="Ürünün son hali " src="https://github.com/user-attachments/assets/fb741a9c-677e-47b3-a98d-32843d63c67c" />
# 💊 Akıllı IoT İlaç Kutusu (Smart IoT Pillbox)



> ESP32 tabanlı, 21 bölmeli (7 gün × 3 öğün), adreslenebilir LED'li, sesli/görsel ikaz sistemine sahip ve internet bağlantılı akıllı ilaç takip kütlesi.

---

## 📌 Proje Hakkında

**Akıllı IoT İlaç Kutusu**, hastaların ve yaşlıların doğru ilacı doğru zamanda almalarını sağlamak, unutkanlığın önüne geçmek ve ilaç alım süreçlerini uzaktan takip edebilmek amacıyla geliştirilmiş açık kaynaklı bir donanım/yazılım projesidir.

### ✨ Öne Çıkan Özellikler
* 🗓️ **21 Bağımsız Bölme:** 7 gün (Pazartesi-Pazar) × 3 öğün (Sabah, Öğlen, Akşam) kapasitesi.
* 🌈 **WS2812B Şerit LED İkazı:** Sadece zamanı gelen ilaç haznesini renklendirerek kullanıcıyı yönlendirir.
* 🖥️ **OLED Arayüz:** Saat, tarih, ortam sıcaklığı ve aktif doz bilgilerini anlık görüntüler.
* 🔊 **Sesli Bildirim (DFPlayer / Buzzer):** İlaç vakti geldiğinde sesli uyarı veya Türkçe konuşma bildirimleri verir.
* 📊 **Kapak Takip Sensörleri:** İlacın gerçekten alınıp alınmadığını teyit eder.
* 🌐 **Wi-Fi & Bulut Entegrasyonu:** NTP sunucusu üzerinden hassas saat takibi ve internet üzerinden veri aktarımı.

---

## 🛠️ Donanım Listesi (BOM - Bill of Materials)

| Bileşen | Adet | Açıklama |
| :--- | :---: | :--- |
| **ESP32 NodeMCU** | 1 | Ana kontrolcü (Wi-Fi + Bluetooth) |
| **2.23" I2C OLED Ekran** | 1 | Durum ve saat bilgi ekranı |
| **WS2812B Adreslenebilir RGB LED** | 1 m (21 LED) | Bölme bazlı görsel ikaz |
| **DFPlayer Mini + Hoparlör** | 1 Set | Sesli ikaz ve mp3 bildirimleri |
| **Kapak Takip Sensörleri** | 21 | Reed Switch / IR Sensör |
| **USB-C Breakout & TP4056** | 1 Set | Güç girişi ve pil şarj yönetimi |
| **3.3V/5V Logic Level Shifter** | 1 | Sinyal seviyesi dönüştürücü |
| **Jumper Kablo & Prototip Board** | - | Devre montaj elemanları |

---

## 📐 Mekanik ve CAD Tasarımı

Cihazın gövdesi **Shapr3D** ortamında özel olarak modellenmiştir.

* **Donanım Haznesi:** Tüm elektronik kartlar, kablo karmaşasını önlemek adına kasanın arkasındaki **3.5 mm** et kalınlığına sahip kapalı bölmede toplanmıştır.
* **Üst Modül:** OLED ekranın dışarıdan rahat okunabilmesi için tavan kısmına özel bir yuva entegre edilmiştir.
* **Üretim:** 3D yazıcı (PLA/PETG) baskısına uygundur.

---

## 🔄 Çalışma Mantığı (System Flow)

```mermaid
graph TD
    A[Cihaz Başlatıldı] --> B[Wi-Fi'a Bağlan & NTP'den Saati Çek]
    B --> C{İlaç Vakti Geldi mi?}
    C -- Hayır --> D[OLED'de Saati Göster & Bekle]
    D --> C
    C -- Evet --> E[İlgili Bölmenin LED'ini Yak]
    E --> F[Sesli İkaz/Alarm Çal]
    F --> G{Kapak Açıldı mı?}
    G -- Hayır --> F
    G -- Evet --> H[LED & Alarmı Kapat]
    H --> I[Buluta 'İlaç Alındı' Bilgisi Gönder]
    I --> D

## 💰 Maliyet Analizi ve Bütçe (BOM & Cost Analysis)

Bu proje için İzmir/Türkiye yerel elektronik tedarikçileri ve piyasa ortalamaları baz alınarak hazırlanan tahmini bütçe tablosu aşağıdadır:

| # | Bileşen / Malzeme | Adet / Miktar | Ortalama Fiyat (TL) | Toplam Tutar |
| :--- | :--- | :---: | :---: | :---: |
| **1** | ESP32 NodeMCU Wi-Fi + BT Geliştirme Kartı | 1 Adet | 220 ₺ | 220 ₺ |
| **2** | 0.96 inç I2C OLED Ekran (128x64) | 1 Adet | 110 ₺ | 110 ₺ |
| **3** | WS2812B Adreslenebilir RGB Şerit LED (60 LED/m) | 1 Metre | 180 ₺ | 180 ₺ |
| **4** | DFPlayer Mini MP3 Modülü + 3W Küçük Hoparlör | 1 Set | 160 ₺ | 160 ₺ |
| **5** | Reed Switch (Mıknatıslı Kapak Sensörü) + Mıknatıs | 21 Set | 15 ₺ / Adet | 315 ₺ |
| **6** | TP4056 Şarj Modülü + USB-C Dişi Breakout Kartı | 1 Set | 65 ₺ | 65 ₺ |
| **7** | 18650 Li-ion Pil (2500 mAh) *(İsteğe Bağlı)* | 1 Adet | 140 ₺ | 140 ₺ |
| **8** | 4-Kanal 3.3V/5V Logic Level Shifter | 1 Adet | 45 ₺ | 45 ₺ |
| **9** | Delikli İki Tarafı Bakır Plaket (Proto-PCB) + Jumper Kablo | 1 Set | 90 ₺ | 90 ₺ |
| **10**| 3D Baskı Filamenti (PLA/PETG ~350g) | ~0.35 kg | 300 ₺ / kg | 105 ₺ |
| **TOPLAM** | **Tahmini Prototip Maliyeti** | | | **~1.430 ₺** |

> 📌 **Not:** Seri üretim aşamasında PCB basımı ve toplu bileşen alımlarıyla birim maliyet **%35-40 oranında düşerek** yaklaşık **850 - 900 ₺** bandına geriletilebilir.

---

## 🛠️ Arka Donanım Haznesi Montaj ve Birleştirme Rehberi

Cihazın arkasındaki **özel kapalı donanım odasına** tüm elektronik modüllerin adım adım nasıl birleştirilip yerleştirileceği aşağıda detaylandırılmıştır:

### 🔌 Step-by-Step Bağlantı ve Montaj Adımları

#### 1. Güç ve Şarj Hattının Kurulumu
* Kasanın yan tarafındaki USB-C portuna dişi soket oturtulur.
* USB-C'den gelen 5V güç hattı **TP4056** şarj modülüne bağlanır.
* 18650 Li-ion pil, TP4056 modülünün `B+` ve `B-` klemenslerine lehimlenir. TP4056'nın `OUT+` çıkışı ise **ESP32'nin VIN (5V)** pinine güç sağlar.

#### 2. Şerit LED ve Hücre Aydınlatması
* WS2812B şerit LED kesilmeden, 21 bölmenin altından yılan (`S` şeklinde) çizerek kesintisiz geçirilir.
* Şerit LED'in **5V ve GND** besleme hatları doğrudan güç devresine bağlanır.
* **Data (DIN)** hattı, ESP32'nin 3.3V sinyalini 5V'a yükselten **Logic Level Shifter** üzerinden `GPIO 16` pinine bağlanır.

#### 3. Ekran ve Ses Modülü Entegrasyonu
* Üst yuvadaki **OLED Ekran** I2C bağlantıları:
  * `SDA` ➔ `GPIO 21`
  * `SCL` ➔ `GPIO 22`
* **DFPlayer Mini** MP3 modülünün TX/RX uçları `GPIO 17` ve `GPIO 16` pinlerine bağlanır. Hoparlör doğrudan DFPlayer üzerindeki ses çıkışlarına lehimlenir.

#### 4. 21 Adet Kapak Sensörünün Matris Bağlantısı
* Sensörlerin pin tasarrufu sağlaması adına Reed Switch'ler **3 Satır × 7 Sütun (Matrix)** yapısında birbirine bağlanır.
* Her kapağın iç kısmına bir neodyum mıknatıs yerleştirilir. Kapak kapandığında devre iletken olur; kapak açıldığında devre kesilerek ESP32'ye "İlaç Alındı" sinyali gönderilir.

#### 5. Donanım Haznesine Sabitleme
* Tüm küçük modüller (ESP32, TP4056, Level Shifter) delikli prototip plakete lehimlenir.
* Plaket, kasanın arkasında yer alan kapalı hazneye M2 vidalar veya sıcak silikon ile sabitlenir.
* Kablo düzeni cırt kelepçelerle sağlandıktan sonra arka kapak kapatılarak montaj tamamlanır.

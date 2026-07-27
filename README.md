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

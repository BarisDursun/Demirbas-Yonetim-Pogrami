# 🏢 SAP ABAP – Demirbaş Yönetim Programı

## 📋 Proje Özeti

Bu proje, **SAP ABAP** ortamında geliştirilmiş bir **Demirbaş & Serbest Stok Yönetim Sistemi**dir. Program, malzemeleri **Serbest Stok** ve **Demirbaş** olarak iki kategoride takip eder ve tek bir buton tıklamasıyla malzemeleri kategoriler arasında transfer etmeyi sağlar.

---

## 🎯 Projenin Amacı

Şirket envanterindeki malzemelerin sınıflandırılması ve yönetimi:

> *"Serbest stoktaki bir malzemeyi demirbaşa çevir veya demirbaş bir malzemeyi serbest stoğa geri al — tek tıklamayla."*

---

## ⚙️ Teknik Detaylar

| Özellik | Detay |
|---|---|
| **Platform** | SAP ERP (ABAP) |
| **Dil** | ABAP (Object-Oriented) |
| **Mimari** | OOP – `lcl_class` sınıfı + Event Handler |
| **Çıktı** | Yan yana 2 ALV Grid (Serbest + Demirbaş) |
| **Veritabanı** | `Z178_DEMRBASYN_T` (tek tablo, flag ile ayrım) |

### 📊 Veritabanı Tablosu

#### `Z178_DEMRBASYN_T` – Demirbaş Yönetim Tablosu

| Alan | Tip | Açıklama |
|---|---|---|
| `MATNR` | CHAR(18) | Malzeme numarası |
| `MAKTX` | CHAR(40) | Malzeme tanımı |
| `LABST` | INT4 | Stok miktarı |
| `DEMIRBAS_MI` | CHAR(1) | `D` = Demirbaş, `S` = Serbest |

---

## 🧠 İş Mantığı

1. Program başlatıldığında `Z178_DEMRBASYN_T` tablosundan veriler çekilir:
   - `DEMIRBAS_MI = 'S'` → **Serbest Raporu** ALV'sine yüklenir
   - `DEMIRBAS_MI = 'D'` → **Demirbaş Raporu** ALV'sine yüklenir
2. Her satırda bir buton bulunur:
   - Serbest tarafta → **"Demirbaşlara Ekle"** butonu
   - Demirbaş tarafta → **"Serbest Stoklara Ekle"** butonu
3. Butona tıklandığında:
   - `DEMIRBAS_MI` alanı güncellenir (`S` ↔ `D`)
   - `UPDATE` komutuyla veritabanı güncellenir
   - Her iki ALV otomatik olarak yenilenir

---

## 🖥️ Ekran Görüntüleri

### Dual ALV Ekranı – Serbest & Demirbaş Raporları

![Dual ALV Ekranı](Resimler/Ekran%20görüntüsü%202026-02-27%20001535.png)

### Veritabanı Tablosu – `Z178_DEMRBASYN_T`

Tablo yapısı (ABAP Dictionary):

![Z178_DEMRBASYN_T Yapısı](Resimler/Ekran%20görüntüsü%202026-02-27%20001420.png)

Tablo verileri:

![Z178_DEMRBASYN_T Verileri](Resimler/Ekran%20görüntüsü%202026-02-27%20001429.png)

---

## 🔑 Öne Çıkan Teknik Özellikler

- **📊 Dual ALV Grid**: Aynı ekranda iki ayrı ALV Grid (Serbest Raporu + Demirbaş Raporu) yan yana görüntülenir.
- **🖱️ ALV Button Click Event**: `handle_button_click` event handler ile buton tıklama aksiyonu yakalanır.
- **🔄 Anlık Veritabanı Güncelleme**: `UPDATE` komutuyla tıklanan malzemenin kategorisi anında değiştirilir.
- **♻️ Otomatik ALV Refresh**: Kategori değişikliğinden sonra her iki ALV otomatik yenilenir.
- **🧩 Yeniden Kullanılabilir Field Catalog**: `insert_to_fcat` metodu ile tekrarlayan fcat tanımlamaları tek metotla yapılır.
- **🏗️ Nesne Yönelimli Mimari (OOP)**: Tüm iş mantığı `lcl_class` sınıfı içinde.

---

## 🛠️ Kullanılan Teknolojiler

`SAP ERP` · `ABAP OOP` · `ALV Grid` · `Event Handler` · `ABAP Dictionary` · `Dynpro` · `Button Click Event`

---

## 📂 Proje Yapısı

```
Z_178_DEMIRBSYON
├── Z_178_DEMIRBSYON_top   → Global veri tanımlamaları, TYPES, Field-Symbols
├── Z_178_DEMIRBSYON_cls   → Sınıf tanımı ve implementasyonu (Event Handler dahil)
└── Z_178_DEMIRBSYON_mdl   → Modül havuzu (PBO/PAI)
```

---

## 👨‍💻 Geliştirici

Bu proje, SAP ABAP eğitimi kapsamında geliştirilmiştir.

---

> **#SAP #ABAP #ALV #DemirbaşYönetimi #AssetManagement #EventHandler #DualALV #OOP #SAPDevelopment #ERPDevelopment**

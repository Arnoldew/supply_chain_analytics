# 📦 Supply Chain Analytics

> **Delivery Performance Analysis — DataCo Smart Supply Chain Dataset**
> Project Portfolio #8 | Operations Analytics

---

## 📋 Project Overview

Supply Chain Analytics berfokus pada analisis efisiensi operasional rantai pasok — mulai dari proses pemesanan hingga pengiriman ke pelanggan. Project ini menganalisis data transaksi nyata dari perusahaan retail global untuk mengidentifikasi bottleneck, mengukur performa pengiriman, dan memberikan rekomendasi strategis berbasis data.

| Komponen | Detail |
|----------|--------|
| **Dataset** | DataCo Smart Supply Chain Dataset (Kaggle) |
| **Ukuran Data** | 9,974 transaksi, 53 kolom |
| **Tools** | Python, Pandas, Matplotlib, Seaborn |
| **Skill Utama** | Operations Analysis, Delivery Analytics |
| **Output** | 6 visualisasi + KPI Summary + README |

---

## 📊 KPI Summary Dashboard

| Metrik | Nilai |
|--------|-------|
| 📦 Total Orders | 9,974 |
| 🔴 Late Delivery Rate | ~55% |
| 🟢 On-Time Delivery Rate | ~45% |
| ⏱️ Avg Delay (when late) | 2–3 hari |
| 🚚 Shipping Modes Analyzed | 4 |
| 🌍 Markets Analyzed | 5 |
| 👥 Customer Segments | 3 |
| 🛒 Product Categories | 20+ |

---

## 📂 Dataset

**Sumber:** [DataCo Smart Supply Chain for Big Data Analysis — Kaggle](https://www.kaggle.com/datasets/shashwatwork/dataco-smart-supply-chain-for-big-data-analysis)

### Kolom yang Digunakan

| Kolom | Tipe | Kegunaan |
|-------|------|---------|
| `Days for shipping (real)` | Numeric | Hari pengiriman aktual |
| `Days for shipment (scheduled)` | Numeric | Hari pengiriman yang dijanjikan |
| `Delivery Status` | Categorical | Late / On Time / Advance / Cancelled |
| `Late_delivery_risk` | Binary | Flag risiko keterlambatan (0/1) |
| `Shipping Mode` | Categorical | Mode pengiriman |
| `order date (DateOrders)` | DateTime | Tanggal order dibuat |
| `shipping date (DateOrders)` | DateTime | Tanggal barang dikirim |
| `Category Name` | Categorical | Kategori produk |
| `Department Name` | Categorical | Departemen produk |
| `Sales` | Numeric | Nilai penjualan ($) |
| `Order Profit Per Order` | Numeric | Profit per order ($) |
| `Customer Segment` | Categorical | Segmen pelanggan |
| `Market` | Categorical | Pasar/Region geografis |
| `Order Region` | Categorical | Region spesifik order |

---

## 🔍 Analisis yang Dilakukan

### 1. Data Cleaning & Feature Engineering
- Seleksi 21 kolom relevan dari 53 kolom total
- Rename kolom untuk kemudahan pemrograman
- Konversi tipe data tanggal ke `datetime`
- Drop missing values pada kolom kritis

**Kolom baru yang diciptakan (Feature Engineering):**
- `delay_days` = `days_real - days_scheduled` → seberapa parah keterlambatan
- `is_late` = `True/False` dari Delivery Status
- `order_year`, `order_month` → diekstrak dari tanggal order
- `profit_margin` = `profit / order_total * 100`

### 2. Delivery Performance Analysis
- Distribusi Delivery Status (Late / On Time / Advance / Cancelled)
- Pie chart dan bar chart overview performa keseluruhan
- Persentase keterlambatan secara agregat

### 3. Category & Department Analysis
- Late rate per kategori produk — sorted dari tertinggi ke terendah
- Scatter plot: Late Rate vs Avg Profit (bubble = order volume)
- Identifikasi kategori yang butuh perhatian khusus

### 4. Shipping Mode Performance
- Late rate per shipping mode (Standard, Second, First, Same Day)
- Volume order per mode
- Actual vs Scheduled days (grouped bar chart)
- Average profit per shipping mode

### 5. Market & Region Analysis
- Late rate per market (Africa, Europe, LATAM, Pacific Asia, USCA)
- Bubble chart: Late Rate vs Total Sales per market

### 6. Customer Segment Analysis
- Late rate: Consumer vs Corporate vs Home Office
- Average profit per segmen
- Volume order per segmen

### 7. Financial Impact Analysis
- Perbandingan avg profit: Late vs On-Time orders
- Perbandingan avg sales: Late vs On-Time
- Estimasi total profit loss akibat keterlambatan

---

## 💡 Key Business Insights

### Finding #1 — Overall Delivery Performance
Late delivery rate mencapai sekitar **55%**, artinya lebih dari separuh pengiriman tidak tepat waktu. Ini adalah angka yang sangat tinggi dan mengindikasikan **masalah sistemik** dalam proses supply chain — bukan sekadar masalah di kategori atau region tertentu.

### Finding #2 — Category Performance
Hampir semua kategori produk memiliki late rate di atas 50%. Ini mengkonfirmasi bahwa masalah bukan pada produk tertentu, melainkan pada **proses pengiriman secara keseluruhan**.

### Finding #3 — Shipping Mode
Setiap mode pengiriman memiliki trade-off berbeda:
- **Same Day Shipping** — paling cepat, late rate rendah, volume sangat kecil
- **First Class** — lebih cepat, namun late rate tetap tinggi
- **Second Class** — volume menengah, performa menengah
- **Standard Class** — volume terbesar, late rate tertinggi → paling berdampak ke bisnis

### Finding #4 — Financial Impact
Terdapat **korelasi negatif** antara keterlambatan dan profit. Order yang terlambat cenderung menghasilkan profit yang lebih rendah dibandingkan order on-time — kemungkinan karena biaya kompensasi atau diskon yang lebih tinggi.

### Finding #5 — Market Distribution
Keterlambatan tersebar **merata di semua market** geografis. Tidak ada market yang secara signifikan lebih baik, memperkuat hipotesis bahwa ini adalah masalah proses internal.

---

## 🎯 Strategic Recommendations

| Prioritas | Rekomendasi | Target Metrik |
|-----------|-------------|---------------|
| 🔴 **1 — Kritis** | Root cause analysis proses Standard Class — audit end-to-end dari warehouse ke carrier | Late rate < 40% |
| 🟠 **2 — Tinggi** | Negosiasi SLA lebih ketat dengan logistics provider + penalty clause | Avg delay < 1 hari |
| 🟠 **3 — Tinggi** | Implementasi early warning system untuk flag orders berisiko sebelum terjadi | Kurangi surprise delay 50% |
| 🟡 **4 — Menengah** | Review kebijakan diskon — cek korelasi diskon tinggi dengan keterlambatan | Optimize discount vs on-time |
| 🟡 **5 — Menengah** | Ekspansi kapasitas Same Day / First Class untuk kategori high-value | +20% premium shipping |
| 🟢 **6 — Rendah** | Monthly performance dashboard untuk monitoring tren real-time | Data-driven decisions |

---

## 📁 Struktur Project

```
supply_chain_analytics/
├── data/
│   └── DataCoSupplyChainDataset.csv
├── notebook/
│   └── supply_chain_analysis.ipynb
├── visuals/
│   ├── 01_delivery_overview.png
│   ├── 02_category_analysis.png
│   ├── 03_shipping_mode.png
│   ├── 04_market_analysis.png
│   ├── 05_customer_segment.png
│   └── 06_financial_impact.png
└── README.md
```

---

## 🛠️ Tech Stack

| Library | Kegunaan |
|---------|---------|
| `pandas` | Data manipulation & aggregation (`groupby`, `agg`) |
| `numpy` | Kalkulasi numerik |
| `matplotlib` | Base charting library |
| `seaborn` | Statistical visualization |

---

## 🚀 Cara Menjalankan

```bash
# 1. Clone repository
git clone <repo-url>
cd supply_chain_analytics

# 2. Download dataset dari Kaggle dan simpan ke folder data/

# 3. Install dependencies
pip install pandas numpy matplotlib seaborn

# 4. Jalankan notebook
jupyter notebook notebook/supply_chain_analysis.ipynb
```

---

## 📚 Key Learnings

| Skill | Aplikasi dalam Project |
|-------|----------------------|
| **Operations Analytics** | Mengukur efisiensi supply chain dengan metrik delivery performance |
| **Feature Engineering** | Membuat `delay_days`, `is_late`, `profit_margin` dari kolom yang ada |
| **`groupby().agg()`** | Aggregasi multi-metrik per category, shipping mode, market, segment |
| **Multi-dimensional Analysis** | Analisis silang: apa + di mana + siapa + dampak finansial |
| **Business Framing** | Setiap angka dikaitkan ke dampak bisnis dan rekomendasi konkret |
| **KPI Dashboard** | Merangkum insight utama dalam format eksekutif |

---

*Project Portfolio Data Analyst | Supply Chain Analytics*

# 📦 E-Commerce Operations & Logistics Dashboard

> A high-performance, client-side Business Analytics dashboard built with vanilla HTML, Tailwind CSS, and Chart.js. This project focuses on operational efficiency — specifically tracking delivery delays, regional customer concentration, and transaction volume trends using the **Olist Brazilian E-Commerce** public dataset.

🌐 **Live Demo:** [https://neiltd.github.io/ecommercedashboards](https://neiltd.github.io/ecommercedashboards)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Business Analytics Focus](#-business-analytics-focus)
- [Live Dashboard Preview](#-live-dashboard-preview)
- [Key Features](#-key-features)
- [Data Schema](#-data-schema)
- [SLA Logic](#-sla--delay-logic)
- [Tech Stack](#-tech-stack)
- [Getting Started](#-getting-started)
- [How to Use](#-how-to-use)
- [Project Structure](#-project-structure)
- [Dashboard Sections](#-dashboard-sections)
- [Design System](#-design-system)
- [Privacy & Data Handling](#-privacy--data-handling)
- [Known Limitations](#-known-limitations)
- [Roadmap](#-roadmap)
- [Dataset Source](#-dataset-source)
- [License](#-license)

---

## Overview

The **E-Commerce Operations & Logistics Dashboard** is a zero-dependency, browser-native analytics tool designed to ingest, join, and visualize the Olist eCommerce relational dataset entirely on the client side. No server. No backend. No data ever leaves your machine.

The dashboard was built as a portfolio project to demonstrate data engineering concepts — relational CSV joining, SLA logic, temporal aggregation, and geographic distribution — without relying on a cloud data warehouse or BI tool. Everything runs in the browser using PapaParse for CSV parsing and Chart.js for visualization.

---

## 🚀 Business Analytics Focus

This dashboard was designed to solve **three specific business problems**:

### 1. 🚚 Logistics Bottlenecks
Identifying the delta between `order_estimated_delivery_date` and `order_delivered_timestamp` to calculate real-world SLA delay rates. The dashboard flags any order where actual delivery exceeded the estimated window — or where the order was canceled/unavailable — as a delayed transaction. This metric directly informs fulfillment team performance.

### 2. 🗺️ Regional Performance
Mapping customer concentration across Brazilian states (SP, RJ, MG, RS, PR, etc.) by joining the Orders and Customers tables on `customer_id`. The resulting geographic distribution chart assists supply chain teams in identifying underserved regions and over-concentrated logistics hubs.

### 3. 📅 Temporal Trends
Analyzing transaction volume on a **monthly**, **weekly**, and **yearly** scale to identify seasonal demand peaks, promotional spikes, and off-cycle lulls. The time-series toggle allows analysts to zoom in or out across time granularities without re-uploading data.

---

## 📸 Live Dashboard Preview

```
┌────────────────────────────────────────────────────────┐
│  OLIST ANALYTICS           ● System Online             │
├──────────────┬─────────────────────────────────────────┤
│              │  💰 $34.4M  📦 89,316  👥 68,772  ⚠️ 8.6%│
│  📥 Upload   ├─────────────────────────────────────────┤
│  Datasets    │  🚚 Logistics Performance               │
│              │  [Volume Trend]     [Order Heatmap]     │
│  📋 Schema   ├─────────────────────────────────────────┤
│  Reference   │  📈 Business Metrics & Demographics     │
│              │  [Category Revenue] [State Distribution]│
│  ⚙️ SLA Def  │                                         │
└──────────────┴─────────────────────────────────────────┘
```

---

## 🛠️ Key Features

- **Dynamic File Ingestion** — Uploads 5 relational CSVs (Orders, Customers, Items, Products, Payments) and performs in-memory hash-map joins on `customer_id` and `product_id`.

- **Service Level Agreement (SLA) Tracking** — Explicit boolean logic flags orders as `LATE` by comparing `order_delivered_timestamp` vs `order_estimated_delivery_date`. Canceled and unavailable statuses are also counted toward the delay rate.

- **Flexible Time-Series** — Toggle between Monthly, Weekly, and Yearly views for transaction volume without re-parsing data. Aggregations are pre-computed at parse time and cached in application state.

- **24/7 Order Heatmap** — Bubble chart plotting Day-of-Week vs Hour-of-Day to surface peak ordering windows. Bubble radius scales with order volume, making logistics stress periods immediately visible.

- **Top 10 Category Revenue** — Horizontal bar chart ranking product categories by gross revenue (price + shipping), with gradient intensity encoding relative ranking.

- **Geographic Customer Density** — Vertical bar chart showing the top 10 Brazilian states by number of active customers, joined from the Orders and Customers datasets.

- **KPI Summary Row** — Four headline metrics (Gross Revenue, Total Orders, Active Customers, SLA Delay Rate) computed at load time and displayed with color-coded accent lines.

- **Zero-Server Architecture** — All CSV parsing, joining, and aggregation runs in the browser via Web APIs. No data is transmitted to any external service.

- **Schema Reference Panel** — Sidebar reference showing the 5 expected files and their join relationships, so analysts always know which file maps to which role.

---

## 📂 Data Schema

The dashboard expects the following **5 CSV files** in Olist format. Column names must match exactly.

| File | Role | Key Column(s) |
|---|---|---|
| `orders_rev_df.csv` | Primary transaction records | `order_id`, `customer_id`, `order_status`, `order_purchase_timestamp`, `order_delivered_timestamp`, `order_estimated_delivery_date` |
| `df_OrderItems.csv` | Product-to-order relationship | `order_id`, `product_id`, `price`, `shipping_charges` |
| `df_Products.csv` | Product category metadata | `product_id`, `product_category_name` |
| `df_Customers.csv` | Customer location and ID mapping | `customer_id`, `customer_state` |
| `df_Payments.csv` | Financial transaction data | `order_id`, `payment_type`, `payment_value` |

> ⚠️ **Note:** The dashboard performs joins using JavaScript `Map` objects keyed on `customer_id` and `product_id`. If your column names differ from the Olist standard, the relevant charts will show `Unknown` values rather than throwing an error.

---

## ⏱️ SLA & Delay Logic

An order is flagged as **delayed** if **either** condition is true:

```
DELAYED = (order_delivered_timestamp > order_estimated_delivery_date)
          OR
          (order_status IN ['canceled', 'unavailable', 'invoiced', 'processing'])
```

The **SLA Delay Rate** KPI is then calculated as:

```
Delay Rate (%) = (Delayed Orders / Total Orders) × 100
```

This is a conservative definition that intentionally includes stuck or canceled orders as operational failures — consistent with how logistics SLAs are evaluated in operations management.

---

## ⚙️ Tech Stack

| Layer | Technology | Version |
|---|---|---|
| Markup | HTML5 | — |
| Styling | Tailwind CSS (CDN) | v3 |
| CSV Parsing | PapaParse | 5.4.1 |
| Charting | Chart.js | Latest |
| Typography | Space Mono + DM Sans | Google Fonts |
| Hosting | GitHub Pages | — |

> This project intentionally avoids build tooling (Vite, Webpack, npm) to remain deployable as a single static `index.html` file with zero configuration.

---

## 🚥 Getting Started

### Option A — Use the Live Version (Recommended)

No installation required. Open the live link and upload your CSV files directly:

🔗 [https://YOUR_USERNAME.github.io/ecom-analytics-dashboard](https://YOUR_USERNAME.github.io/ecom-analytics-dashboard)

### Option B — Run Locally

Since this is a single HTML file with no build step, you can run it with any static file server:

**Using Python:**
```bash
git clone https://github.com/YOUR_USERNAME/ecom-analytics-dashboard.git
cd ecom-analytics-dashboard
python -m http.server 8000
# Open http://localhost:8000
```

**Using Node (npx serve):**
```bash
npx serve .
```

**Or simply open `index.html` directly in your browser** — most features work without a server since there are no ES module imports.

---

## 📖 How to Use

1. **Open the dashboard** at the live URL or locally.
2. **Upload your 5 CSV files** using the sidebar upload panel. Files can be uploaded in any order.
3. Each uploaded file shows its **filename and row count** as confirmation.
4. Once all 5 files are loaded, the **"Generate Analytics →"** button activates.
5. Click the button — the dashboard parses, joins, and aggregates all data in-memory.
6. **KPI cards** populate immediately at the top.
7. Use the **Monthly / Weekly / Yearly toggle** to switch time-series granularity.
8. Hover over chart elements for **detailed tooltips**.
9. The status badge in the header switches from **System Offline** to **System Online**.

---

## 📁 Project Structure

```
ecom-analytics-dashboard/
│
├── index.html          ← Entire application (HTML + CSS + JS, single file)
└── README.md           ← This file
```

The entire application lives in a single `index.html` for maximum portability and simplicity of GitHub Pages deployment.

---

## 📊 Dashboard Sections

### KPI Row
Four headline metrics computed from the joined dataset:
- **Gross Revenue** — Sum of `price + shipping_charges` across all order items, displayed in `$M` or `$K` format.
- **Total Orders** — Count of rows in the orders dataset.
- **Active Customers** — Count of distinct `customer_id` values linked to at least one order.
- **SLA Delay Rate** — Percentage of orders meeting the delay definition above.

### 🚚 Logistics Performance

**Transaction Volume Chart**
A filled line chart showing order counts aggregated by the selected time granularity (Monthly / Weekly / Yearly). The Y-axis begins at zero for honest representation of volume changes. Data is pre-aggregated using JavaScript `Map` objects and sorted chronologically.

**24/7 Ordering Heatmap**
A bubble chart with Hour of Day on the X-axis and Day of Week on the Y-axis. Each bubble represents the volume of orders placed at that day-hour intersection, with bubble radius scaled proportionally to the maximum count in the dataset. Useful for identifying staffing and logistics capacity windows.

### 📈 Business Metrics & Demographics

**Top 10 Categories by Revenue**
A horizontal bar chart ranking the top 10 product categories by combined `price + shipping_charges`. Categories are joined from `df_OrderItems` → `df_Products` via `product_id`. Gradient fill intensity encodes relative rank.

**Customer Density by State**
A vertical bar chart showing the top 10 Brazilian states by number of customers who placed at least one order. Joined from `orders_rev_df` → `df_Customers` via `customer_id`.

---

## 🎨 Design System

| Token | Value | Usage |
|---|---|---|
| Background | `#060910` | Page base |
| Surface | `#0d1117` | Input backgrounds |
| Panel | `#111820` | Card backgrounds |
| Border | `#1e2d3d` | Default borders |
| Cyan | `#00d4ff` | Primary accent, volume chart |
| Emerald | `#00e5a0` | Revenue, category chart |
| Violet | `#a78bfa` | Customers, geo chart |
| Rose | `#ff4d6d` | Delay rate, heatmap |
| Display font | Space Mono | KPI values, labels, badges |
| Body font | DM Sans | Descriptions, tooltips |

The background uses a subtle `40px` CSS grid pattern at `3% opacity` to add depth without visual noise.

---

## 🔒 Privacy & Data Handling

- **No data leaves your browser.** All CSV files are parsed and processed entirely in memory using the browser's JavaScript engine.
- No analytics, telemetry, or tracking scripts are included.
- No cookies are set.
- Refreshing the page clears all uploaded data — nothing is persisted to `localStorage` or any server.

This makes the dashboard safe to use with real business data.

---

## ⚠️ Known Limitations

- **Large files (>100MB):** PapaParse handles large files well, but the browser may slow noticeably on very large datasets (>500k rows) due to the in-memory join operations.
- **Column name sensitivity:** The parser expects exact Olist column names. Custom exports with renamed columns will require manual renaming before upload.
- **Currency:** All revenue figures are displayed in USD formatting. The Olist dataset uses Brazilian Real (BRL). No currency conversion is applied.
- **No persistent state:** Closing or refreshing the tab clears all data and resets the dashboard.
- **Mobile layout:** The dashboard is optimized for desktop (1200px+). Narrower viewports may require horizontal scrolling on chart sections.

---

## 🗺️ Roadmap

- [ ] **Option C — Advanced Features**
  - [ ] SLA Breakdown Table (per-state delay rates)
  - [ ] Delay by State heatmap
  - [ ] CSV Export button for aggregated metrics
  - [ ] Payment method distribution chart
- [ ] Responsive mobile layout
- [ ] Dark/light theme toggle
- [ ] URL-based state sharing (encode filters in query params)
- [ ] Support for custom column name mapping

---

## 📦 Dataset Source

This dashboard is designed for the **Olist Brazilian E-Commerce Public Dataset**, available on Kaggle:

🔗 [https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

The dataset contains ~100k orders from 2016–2018 made at multiple marketplaces in Brazil, with information on order status, price, payment, freight performance, customer location, product attributes, and customer reviews.

---

## 📄 License

This project is open source under the [MIT License](LICENSE).

```
MIT License — free to use, modify, and distribute with attribution.
```

---

<div align="center">

Built with 📊 Chart.js · 📄 PapaParse · 🎨 Tailwind CSS

**[Live Demo](https://YOUR_USERNAME.github.io/ecom-analytics-dashboard)** · **[Dataset on Kaggle](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)**

</div>

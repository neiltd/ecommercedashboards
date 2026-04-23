E-Commerce Operations & Logistics Dashboard

A high-performance Business Analytics dashboard built with React and Tailwind CSS. This project focuses on operational efficiency, specifically tracking delivery delays and customer acquisition trends using the Olist eCommerce dataset.

🚀 Business Analytics Focus

This dashboard was designed to solve three specific business problems:

Logistics Bottlenecks: Identifying the delta between estimated and actual delivery timestamps to calculate real-world delay rates.

Regional Performance: Mapping customer concentration across Brazilian states (SP, RJ, MG, etc.) to assist in supply chain optimization.

Temporal Trends: Analyzing transaction volume on a monthly and yearly scale to identify seasonal peaks.

🛠️ Key Features

Dynamic File Ingestion: Uploads 5 relational CSVs (Orders, Customers, Items, Products, Payments) and joins them in-memory.

Service Level Agreement (SLA) Tracking: Explicit logic to flag 'Late' orders by comparing order_delivered_timestamp vs order_estimated_delivery_date.

Flexible Time-Series: Toggle between Monthly and Yearly views for transaction volume.

Geographic Distribution: State-level breakdown of the active customer base.

📂 Data Schema

The dashboard expects the following files (Olist Format):

order_rev_df: Primary transaction records.

df_customer: Customer location and ID mapping.

df_orderitem: Product-to-order relationship.

df_product: Category metadata.

df_payment: Financial transaction data.

⚙️ Tech Stack

Framework: React.js (Vite)

Styling: Tailwind CSS

Visualization: Recharts

Icons: Lucide React

🚥 Getting Started

Clone the repo: git clone https://github.com/yourusername/ecom-analytics-dashboard.git

Install dependencies: npm install

Run locally: npm run dev

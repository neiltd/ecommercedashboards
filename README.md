<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>E-Commerce Operations & Logistics Dashboard Documentation</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700;900&display=swap');
        body {
            font-family: 'Inter', sans-serif;
            background-color: #0b0e14;
        }
        .glass-card {
            background: rgba(15, 23, 42, 0.6);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.1);
        }
    </style>
</head>
<body class="text-slate-300 leading-relaxed antialiased">
    <div class="max-w-4xl mx-auto px-6 py-16">
        <!-- Header -->
        <header class="mb-16">
            <h1 class="text-5xl font-black tracking-tight text-white italic uppercase mb-6">
                E-COMM <span class="text-cyan-400">ANALYTICS</span> DASHBOARD
            </h1>
            <p class="text-xl text-slate-400">
                This React dashboard analyzes e-commerce operations using the Olist dataset. It tracks logistics by flagging late deliveries and maps customer density across states to help optimize supply chains. Users can filter transaction trends by month or year, turning raw CSVs into clear insights on operational health and regional demand.
            </p>
        </header>

        <!-- Business Focus -->
        <section class="mb-12">
            <h2 class="text-2xl font-bold text-white mb-6 flex items-center gap-3">
                <span class="text-cyan-400">🚀</span> Business Analytics Focus
            </h2>
            <div class="grid gap-4">
                <div class="glass-card p-6 rounded-2xl">
                    <h3 class="font-bold text-white mb-2">1. Logistics Bottlenecks</h3>
                    <p class="text-sm">Identifying the delta between estimated and actual delivery timestamps to calculate real-world delay rates.</p>
                </div>
                <div class="glass-card p-6 rounded-2xl">
                    <h3 class="font-bold text-white mb-2">2. Regional Performance</h3>
                    <p class="text-sm">Mapping customer concentration across Brazilian states (SP, RJ, MG, etc.) to assist in supply chain optimization.</p>
                </div>
                <div class="glass-card p-6 rounded-2xl">
                    <h3 class="font-bold text-white mb-2">3. Temporal Trends</h3>
                    <p class="text-sm">Analyzing transaction volume on a monthly and yearly scale to identify seasonal peaks.</p>
                </div>
            </div>
        </section>

        <!-- Key Features -->
        <section class="mb-12">
            <h2 class="text-2xl font-bold text-white mb-6 flex items-center gap-3">
                <span class="text-cyan-400">🛠️</span> Key Features
            </h2>
            <ul class="space-y-3 list-disc list-inside bg-slate-900/30 p-6 rounded-2xl border border-slate-800">
                <li><strong class="text-slate-100">Dynamic File Ingestion:</strong> Uploads 5 relational CSVs and joins them in-memory.</li>
                <li><strong class="text-slate-100">SLA Tracking:</strong> Logic to flag 'Late' orders by comparing delivered vs. estimated dates.</li>
                <li><strong class="text-slate-100">Flexible Time-Series:</strong> Toggle between Monthly and Yearly views.</li>
                <li><strong class="text-slate-100">Geographic Distribution:</strong> State-level breakdown of the active customer base.</li>
                <li><strong class="text-slate-100">Interactive Date Filtering:</strong> Real-time chart updates based on custom selections.</li>
            </ul>
        </section>

        <!-- Data Schema -->
        <section class="mb-12">
            <h2 class="text-2xl font-bold text-white mb-6 flex items-center gap-3">
                <span class="text-cyan-400">📂</span> Data Schema
            </h2>
            <div class="overflow-hidden border border-slate-800 rounded-2xl">
                <table class="w-full text-left text-sm">
                    <thead class="bg-slate-900 text-slate-400 uppercase text-[10px] tracking-widest">
                        <tr>
                            <th class="px-6 py-3">File Name</th>
                            <th class="px-6 py-3">Description</th>
                        </tr>
                    </thead>
                    <tbody class="divide-y divide-slate-800 bg-slate-950/50">
                        <tr>
                            <td class="px-6 py-4 font-mono text-cyan-400">orders_rev_df</td>
                            <td class="px-6 py-4">Primary transaction records</td>
                        </tr>
                        <tr>
                            <td class="px-6 py-4 font-mono text-cyan-400">df_customer</td>
                            <td class="px-6 py-4">Customer location and ID mapping</td>
                        </tr>
                        <tr>
                            <td class="px-6 py-4 font-mono text-cyan-400">df_orderitem</td>
                            <td class="px-6 py-4">Product-to-order relationship</td>
                        </tr>
                        <tr>
                            <td class="px-6 py-4 font-mono text-cyan-400">df_product</td>
                            <td class="px-6 py-4">Category metadata</td>
                        </tr>
                        <tr>
                            <td class="px-6 py-4 font-mono text-cyan-400">df_payment</td>
                            <td class="px-6 py-4">Financial transaction data</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </section>

        <!-- Tech Stack -->
        <section class="mb-12">
            <h2 class="text-2xl font-bold text-white mb-6 flex items-center gap-3">
                <span class="text-cyan-400">⚙️</span> Tech Stack
            </h2>
            <div class="flex flex-wrap gap-3">
                <span class="px-4 py-2 bg-slate-800 rounded-full text-xs font-bold text-slate-300 border border-slate-700">React.js (Vite)</span>
                <span class="px-4 py-2 bg-slate-800 rounded-full text-xs font-bold text-slate-300 border border-slate-700">Tailwind CSS</span>
                <span class="px-4 py-2 bg-slate-800 rounded-full text-xs font-bold text-slate-300 border border-slate-700">Recharts</span>
                <span class="px-4 py-2 bg-slate-800 rounded-full text-xs font-bold text-slate-300 border border-slate-700">Lucide React</span>
            </div>
        </section>

        <!-- Getting Started -->
        <section class="mb-12">
            <h2 class="text-2xl font-bold text-white mb-6">🚥 Getting Started</h2>
            <div class="space-y-6">
                <div>
                    <p class="mb-3 text-sm font-semibold text-slate-400">1. Clone the repo</p>
                    <pre class="bg-slate-950 p-4 rounded-xl border border-slate-800 overflow-x-auto"><code class="text-cyan-400 text-xs">git clone https://github.com/yourusername/ecom-analytics-dashboard.git
cd ecom-analytics-dashboard</code></pre>
                </div>
                <div>
                    <p class="mb-3 text-sm font-semibold text-slate-400">2. Install dependencies</p>
                    <pre class="bg-slate-950 p-4 rounded-xl border border-slate-800 overflow-x-auto"><code class="text-cyan-400 text-xs">npm install</code></pre>
                </div>
                <div>
                    <p class="mb-3 text-sm font-semibold text-slate-400">3. Run locally</p>
                    <pre class="bg-slate-950 p-4 rounded-xl border border-slate-800 overflow-x-auto"><code class="text-cyan-400 text-xs">npm run dev</code></pre>
                </div>
            </div>
        </section>

        <!-- Methodology -->
        <section class="mb-12 bg-cyan-500/5 border border-cyan-500/20 p-8 rounded-[32px]">
            <h2 class="text-2xl font-bold text-white mb-4 flex items-center gap-3">
                <span class="text-cyan-400">📊</span> Methodology: Delay Rate
            </h2>
            <p class="text-sm mb-6">The <strong>Delay Rate</strong> is calculated using a comprehensive logic gate:</p>
            <ul class="space-y-4 text-sm">
                <li class="flex items-start gap-3">
                    <div class="mt-1.5 w-1.5 h-1.5 rounded-full bg-cyan-400 shrink-0"></div>
                    <span><strong class="text-white">Status Check:</strong> Any order with a status of <em>canceled</em> or <em>unavailable</em> is flagged as a business-process delay.</span>
                </li>
                <li class="flex items-start gap-3">
                    <div class="mt-1.5 w-1.5 h-1.5 rounded-full bg-cyan-400 shrink-0"></div>
                    <span><strong class="text-white">Timestamp Comparison:</strong> For delivered orders, the system parses the <code class="bg-slate-900 px-1 rounded text-cyan-400">order_delivered_timestamp</code> and compares it against the <code class="bg-slate-900 px-1 rounded text-cyan-400">order_estimated_delivery_date</code>.</span>
                </li>
                <li class="flex items-start gap-3">
                    <div class="mt-1.5 w-1.5 h-1.5 rounded-full bg-cyan-400 shrink-0"></div>
                    <span><strong class="text-white">Formula:</strong> <code class="bg-slate-900 px-1 rounded text-cyan-400">(Delayed Orders / Total Transactions) * 100</code></span>
                </li>
            </ul>
        </section>
    </div>
</body>
</html>

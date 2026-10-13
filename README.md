# Amazon-Front-End-Crawl
Bed sheet Analysis (Amazon)
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Amazon.in King Size Cotton Bedsheet Market Analysis</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    :root {
      --bg: #f8fafc;
      --card: #ffffff;
      --text: #1e293b;
      --muted: #64748b;
      --border: #e2e8f0;
      --green: #10b981;
      --green-bg: #dcfce7;
      --green-text: #166534;
      --red: #ef4444;
      --red-bg: #fee2e2;
      --red-text: #991b1b;
      --amber: #f59e0b;
    }
    * { box-sizing: border-box; }
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
      background: var(--bg);
      color: var(--text);
      margin: 0;
      padding: 2rem 1rem;
      line-height: 1.5;
    }
    .container {
      max-width: 1100px;
      margin: 0 auto;
      background: var(--card);
      padding: 2rem;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
      border: 1px solid var(--border);
    }
    h1 { margin: 0 0 0.5rem 0; font-size: 1.75rem; color: #0f172a; }
    .subtitle { color: var(--muted); margin-bottom: 1.75rem; font-size: 0.95rem; }
    
    /* KPI Cards */
    .kpi-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 1rem;
      margin-bottom: 1.75rem;
    }
    .kpi-card {
      padding: 1rem 1.25rem;
      border-radius: 8px;
      border: 1px solid var(--border);
      background: #f8fafc;
    }
    .kpi-label { font-size: 0.8rem; text-transform: uppercase; letter-spacing: 0.04em; color: var(--muted); font-weight: 600; }
    .kpi-val { font-size: 1.5rem; font-weight: 700; margin-top: 0.25rem; }
    .kpi-sub { font-size: 0.8rem; color: var(--muted); margin-top: 0.2rem; }

    /* Controls */
    .controls {
      display: flex;
      flex-wrap: wrap;
      gap: 1rem;
      align-items: center;
      justify-content: space-between;
      background: #f1f5f9;
      padding: 1rem 1.25rem;
      border-radius: 8px;
      margin-bottom: 1.5rem;
    }
    .control-group {
      display: flex;
      align-items: center;
      gap: 0.5rem;
      font-size: 0.9rem;
      font-weight: 500;
    }
    select, input[type="range"] {
      padding: 0.4rem 0.6rem;
      border-radius: 6px;
      border: 1px solid #cbd5e1;
      background: white;
      font-size: 0.9rem;
    }
    .chart-wrapper {
      position: relative;
      height: 460px;
      width: 100%;
      margin-bottom: 2rem;
    }

    /* Table */
    .table-container { overflow-x: auto; }
    table {
      width: 100%;
      border-collapse: collapse;
      font-size: 0.9rem;
    }
    th, td {
      border-bottom: 1px solid var(--border);
      padding: 0.75rem 0.85rem;
      text-align: left;
    }
    th {
      background: #f1f5f9;
      font-weight: 600;
      color: #334155;
      position: sticky;
      top: 0;
    }
    tr:hover { background: #f8fafc; }
    .badge {
      display: inline-block;
      padding: 0.2rem 0.6rem;
      border-radius: 999px;
      font-size: 0.75rem;
      font-weight: 600;
    }
    .badge-cotton { background: var(--green-bg); color: var(--green-text); }
    .badge-poly { background: var(--red-bg); color: var(--red-text); }
    .callout {
      margin-top: 1.75rem;
      padding: 1rem 1.25rem;
      background: #fffbeb;
      border-left: 4px solid var(--amber);
      border-radius: 6px;
      font-size: 0.9rem;
      color: #92400e;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Amazon.in: "Cotton Bedsheet for King Size Bed" Analysis</h1>
    <p class="subtitle">Market breakdown comparing product title claims vs. actual technical fabric specs, pricing tiers, and Thread Count (TC) / GSM metrics.</p>

    <div class="kpi-grid">
      <div class="kpi-card">
        <div class="kpi-label">True Cotton Price Floor</div>
        <div class="kpi-val" style="color: #d97706;">₹750 – ₹799</div>
        <div class="kpi-sub">Sheets under ₹750 are almost all polyester</div>
      </div>
      <div class="kpi-card">
        <div class="kpi-label">Synthetic / Glacé Avg Price</div>
        <div class="kpi-val" style="color: var(--red);">₹480</div>
        <div class="kpi-sub">Range: ₹299 – ₹799 (Microfiber / Blends)</div>
      </div>
      <div class="kpi-card">
        <div class="kpi-label">100% Pure Cotton Avg Price</div>
        <div class="kpi-val" style="color: var(--green);">₹1,550</div>
        <div class="kpi-sub">Range: ₹799 – ₹2,999 (144 TC to 300 TC)</div>
      </div>
    </div>

    <div class="controls">
      <div class="control-group">
        <label for="viewToggle">Chart View:</label>
        <select id="viewToggle">
          <option value="bar">Brand Price Ranking (Bar)</option>
          <option value="scatter">Price vs. Claimed TC (Scatter)</option>
        </select>
      </div>
      <div class="control-group">
        <label for="materialFilter">Actual Material:</label>
        <select id="materialFilter">
          <option value="all">All Brands (19)</option>
          <option value="cotton">100% Pure Cotton Only</option>
          <option value="poly">Synthetic / Glacé Microfiber Only</option>
        </select>
      </div>
      <div class="control-group">
        <label for="budgetSlider">Max Price: <strong id="budgetValue">₹3,000</strong></label>
        <input type="range" id="budgetSlider" min="300" max="3000" step="50" value="3000">
      </div>
    </div>

    <div class="chart-wrapper">
      <canvas id="marketChart"></canvas>
    </div>

    <div class="table-container">
      <table>
        <thead>
          <tr>
            <th>Brand</th>
            <th>Mentioned Material (Title)</th>
            <th>Actual Material (Spec Sheet)</th>
            <th>Metric Used</th>
            <th>Claimed Spec</th>
            <th>King Price (₹)</th>
          </tr>
        </thead>
        <tbody id="tableBody"></tbody>
      </table>
    </div>

    <div class="callout">
      <strong>How to spot fake cotton on Amazon.in:</strong> Ignore "Glacé Cotton" or "100% Cotton Feel" in the title. Scroll to <em>Product Information → Technical Details → Material</em>. If a king-size bedsheet claims <strong>250–400 TC under ₹600</strong>, it is brushed polyester microfiber (110–140 GSM), not woven cotton.
    </div>
  </div>

  <script>
    const rawData = [
      { brand: "BSB HOME", title: "100% Cotton Feel / Glacé Cotton", actual: "100% Polyester (Microfiber)", group: "poly", metric: "Both (Fake TC + GSM)", tc: 160, gsm: 140, spec: "160 TC / 140 GSM", price: 299 },
      { brand: "HOMEKART", title: "Supersoft Microfiber Cotton Feel", actual: "100% Polyester (Microfiber)", group: "poly", metric: "TC (Fake)", tc: 144, gsm: 120, spec: "144 TC (120 GSM)", price: 309 },
      { brand: "VAS COLLECTIONS", title: "Comfort Panipat Glacé Cotton", actual: "Polycotton / Microfiber", group: "poly", metric: "TC (Fake)", tc: 160, gsm: 130, spec: "160 TC", price: 319 },
      { brand: "BM DECOR", title: "Glacé Cotton Fitted", actual: "100% Polyester (Brushed Microfiber)", group: "poly", metric: "TC (Fake)", tc: 254, gsm: 140, spec: "254 TC", price: 419 },
      { brand: "KIJO Home", title: "Supersoft Cotton Feel Glacé Cotton", actual: "100% Polyester (Microfiber)", group: "poly", metric: "TC (Inflated Fake)", tc: 400, gsm: 150, spec: "400 TC", price: 499 },
      { brand: "Home Sizzler", title: "Cotton Feel Botanical", actual: "100% Polyester (Microfiber)", group: "poly", metric: "TC (Fake)", tc: 210, gsm: 140, spec: "210 TC", price: 549 },
      { brand: "Linemates", title: "Soft Glacé Cotton Printed", actual: "Polyester / Glacé Microfiber", group: "poly", metric: "TC (Fake)", tc: 160, gsm: 140, spec: "160 TC", price: 649 },
      { brand: "Furnofy", title: "Cotton-Soft Flat Sheet", actual: "100% Polyester (Microfiber)", group: "poly", metric: "GSM (Accurate)", tc: 140, gsm: 140, spec: "140 GSM", price: 799 },
      { brand: "Story@Home", title: "100% Cotton", actual: "100% Pure Cotton", group: "cotton", metric: "TC (Cotton) / GSM (Microfiber)", tc: 260, gsm: 160, spec: "260 TC", price: 799 },
      { brand: "Amazon Brand - Solimo", title: "100% Cotton", actual: "100% Pure Cotton", group: "cotton", metric: "TC", tc: 144, gsm: 140, spec: "144 TC", price: 839 },
      { brand: "Huesland", title: "100% Comfort Cotton", actual: "100% Pure Cotton", group: "cotton", metric: "TC", tc: 144, gsm: 145, spec: "144 TC", price: 986 },
      { brand: "Spaces", title: "100% Cotton Superfine", actual: "100% Pure Cotton", group: "cotton", metric: "TC", tc: 144, gsm: 150, spec: "144 TC", price: 1049 },
      { brand: "JaipurFabric", title: "100% Cotton Rajasthani Jaipuri", actual: "100% Pure Cotton", group: "cotton", metric: "TC", tc: 240, gsm: 160, spec: "240 TC", price: 1199 },
      { brand: "Wakefit", title: "Cotton Fitted / Micro-peach", actual: "100% Pure Cotton", group: "cotton", metric: "TC (Cotton) / GSM (Microfiber)", tc: 200, gsm: 150, spec: "200 TC", price: 1280 },
      { brand: "Bombay Dyeing", title: "100% Pure Cotton", actual: "100% Pure Cotton", group: "cotton", metric: "TC", tc: 144, gsm: 150, spec: "144 TC", price: 1549 },
      { brand: "haus & kinder", title: "100% Cotton", actual: "100% Pure Cotton", group: "cotton", metric: "TC", tc: 186, gsm: 155, spec: "186 TC", price: 1799 },
      { brand: "elaris (Sponsored)", title: "300 TC Cotton", actual: "100% Pure Cotton (Sateen)", group: "cotton", metric: "TC", tc: 300, gsm: 180, spec: "300 TC", price: 2199 },
      { brand: "ARiANA / Blue Dahlia", title: "100% Cotton Sateen", actual: "100% Pure Cotton (Sateen)", group: "cotton", metric: "TC", tc: 300, gsm: 185, spec: "300 TC", price: 2350 },
      { brand: "D'Decor", title: "Live Beautiful Cotton", actual: "100% Pure Cotton", group: "cotton", metric: "TC", tc: 210, gsm: 170, spec: "210 TC", price: 2999 }
    ];

    let chartInstance = null;
    const ctx = document.getElementById('marketChart').getContext('2d');
    const viewToggle = document.getElementById('viewToggle');
    const materialFilter = document.getElementById('materialFilter');
    const budgetSlider = document.getElementById('budgetSlider');
    const budgetValue = document.getElementById('budgetValue');
    const tableBody = document.getElementById('tableBody');

    function render() {
      const mode = viewToggle.value;
      const mat = materialFilter.value;
      const maxPrice = parseInt(budgetSlider.value, 10);
      budgetValue.textContent = `₹${maxPrice.toLocaleString('en-IN')}`;

      const filtered = rawData.filter(d => {
        const matMatch = mat === 'all' || d.group === mat;
        return matMatch && d.price <= maxPrice;
      });

      // Render Table
      tableBody.innerHTML = filtered.map(d => `
        <tr>
          <td><strong>${d.brand}</strong></td>
          <td>${d.title}</td>
          <td><span class="badge ${d.group === 'cotton' ? 'badge-cotton' : 'badge-poly'}">${d.actual}</span></td>
          <td>${d.metric}</td>
          <td>${d.spec}</td>
          <td><strong>₹${d.price.toLocaleString('en-IN')}</strong></td>
        </tr>
      `).join('');

      if (chartInstance) chartInstance.destroy();

      if (mode === 'bar') {
        chartInstance = new Chart(ctx, {
          type: 'bar',
          data: {
            labels: filtered.map(d => d.brand),
            datasets: [{
              label: 'Price (₹ INR)',
              data: filtered.map(d => d.price),
              backgroundColor: filtered.map(d => d.group === 'cotton' ? '#10b981' : '#ef4444'),
              borderRadius: 4
            }]
          },
          options: {
            indexAxis: 'y',
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
              legend: { display: false },
              tooltip: {
                callbacks: {
                  label: (ctx) => {
                    const item = filtered[ctx.dataIndex];
                    return ` ₹${item.price} | Actual: ${item.actual} | Claimed: ${item.spec}`;
                  }
                }
              }
            },
            scales: {
              x: { title: { display: true, text: 'Selling Price in ₹ INR (Red = Synthetic/Glacé, Green = 100% Pure Cotton)' } }
            }
          }
        });
      } else {
        const cottonPts = filtered.filter(d => d.group === 'cotton').map(d => ({ x: d.tc, y: d.price, item: d }));
        const polyPts = filtered.filter(d => d.group === 'poly').map(d => ({ x: d.tc, y: d.price, item: d }));

        chartInstance = new Chart(ctx, {
          type: 'scatter',
          data: {
            datasets: [
              {
                label: '100% Pure Cotton',
                data: cottonPts,
                backgroundColor: '#10b981',
                pointRadius: 7
              },
              {
                label: 'Synthetic / Glacé Microfiber (Fake TC)',
                data: polyPts,
                backgroundColor: '#ef4444',
                pointRadius: 7
              }
            ]
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            plugins: {
              tooltip: {
                callbacks: {
                  label: (ctx) => {
                    const d = ctx.raw.item;
                    return `${d.brand}: ₹${d.price} (${d.spec}) — ${d.actual}`;
                  }
                }
              }
            },
            scales: {
              x: { title: { display: true, text: 'Claimed Thread Count (TC)' }, min: 100, max: 430 },
              y: { title: { display: true, text: 'Selling Price (₹ INR)' }, min: 0 }
            }
          }
        });
      }
    }

    viewToggle.addEventListener('change', render);
    materialFilter.addEventListener('change', render);
    budgetSlider.addEventListener('input', render);
    render();
  </script>
</body>
</html>

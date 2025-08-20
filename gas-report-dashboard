<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Our City C-Store Gas Report</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #e6f0ff;
      color: #003366;
      margin: 0;
      padding: 0;
    }
    header {
      background-color: #0059b3;
      color: white;
      padding: 20px;
      text-align: center;
    }
    main {
      padding: 20px;
    }
    .dashboard {
      display: flex;
      flex-wrap: wrap;
      gap: 20px;
      justify-content: space-around;
      margin-bottom: 20px;
    }
    .dashboard div {
      background-color: #cce0ff;
      padding: 20px;
      border-radius: 10px;
      flex: 1 1 250px;
      text-align: center;
    }
    table {
      width: 100%;
      border-collapse: collapse;
      margin-bottom: 20px;
    }
    th, td {
      border: 1px solid #003366;
      padding: 10px;
      text-align: center;
    }
    th {
      background-color: #99c2ff;
    }
    canvas {
      background-color: #ffffff;
      border: 1px solid #003366;
      border-radius: 10px;
      display: block;
      margin: 0 auto;
    }
    button {
      background-color: #0059b3;
      color: white;
      padding: 10px 20px;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      margin-bottom: 20px;
    }
    button:hover {
      background-color: #004080;
    }
  </style>
</head>
<body>
  <header>
    <h1>Our City C-Store Gas Report</h1>
  </header>
  <main>
    <section class="dashboard">
      <div>
        <h2>Total Sales Today</h2>
        <p id="totalSales">0 gal</p>
      </div>
      <div>
        <h2>Remaining Inventory</h2>
        <p id="remainingInventory">Regular: 4000, Ethanol: 8000, Premium: 4000</p>
      </div>
      <div>
        <h2>Daily Summary</h2>
        <p id="dailySummary">-</p>
      </div>
    </section>

    <h2>Daily Sales Entry</h2>
    <table>
      <thead>
        <tr>
          <th>Date</th>
          <th>Regular Sold (gal)</th>
          <th>Ethanol Sold (gal)</th>
          <th>Premium Sold (gal)</th>
        </tr>
      </thead>
      <tbody id="salesTable">
        <tr>
          <td contenteditable="true">2025-08-20</td>
          <td contenteditable="true">0</td>
          <td contenteditable="true">0</td>
          <td contenteditable="true">0</td>
        </tr>
      </tbody>
    </table>
    <button onclick="updateInventory()">Update Inventory</button>

    <h2>Sales Trend Chart</h2>
    <canvas id="salesChart" width="600" height="300"></canvas>
  </main>

  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script>
    let inventory = { regular: 4000, ethanol: 8000, premium: 4000 };
    let salesData = [];

    function updateInventory() {
      const table = document.getElementById('salesTable');
      const row = table.rows[0];
      const date = row.cells[0].innerText;
      const regularSold = parseInt(row.cells[1].innerText) || 0;
      const ethanolSold = parseInt(row.cells[2].innerText) || 0;
      const premiumSold = parseInt(row.cells[3].innerText) || 0;

      inventory.regular -= regularSold;
      inventory.ethanol -= ethanolSold;
      inventory.premium -= premiumSold;

      document.getElementById('totalSales').innerText = (regularSold + ethanolSold + premiumSold) + ' gal';
      document.getElementById('remainingInventory').innerText = `Regular: ${inventory.regular}, Ethanol: ${inventory.ethanol}, Premium: ${inventory.premium}`;
      document.getElementById('dailySummary').innerText = `Regular: ${regularSold}, Ethanol: ${ethanolSold}, Premium: ${premiumSold}`;

      salesData.push({ date, regular: regularSold, ethanol: ethanolSold, premium: premiumSold });
      renderChart();
    }

    function renderChart() {
      const labels = salesData.map(entry => entry.date);
      const regularSales = salesData.map(entry => entry.regular);
      const ethanolSales = salesData.map(entry => entry.ethanol);
      const premiumSales = salesData.map(entry => entry.premium);

      const ctx = document.getElementById('salesChart').getContext('2d');
      new Chart(ctx, {
        type: 'line',
        data: {
          labels: labels,
          datasets: [
            {
              label: 'Regular',
              data: regularSales,
              borderColor: '#3366cc',
              fill: false
            },
            {
              label: 'Ethanol',
              data: ethanolSales,
              borderColor: '#66cc66',
              fill: false
            },
            {
              label: 'Premium',
              data: premiumSales,
              borderColor: '#cc3333',
              fill: false
            }
          ]
        },
        options: {
          responsive: true,
          plugins: {
            legend: { position: 'top' },
            title: { display: true, text: 'Gas Sales Trend' }
          }
        }
      });
    }
  </script>
</body>
</html>

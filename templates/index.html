<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>天氣 — {{ weather.city }}</title>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.min.js"></script>
  <style>
    * { box-sizing: border-box; margin: 0; padding: 0; }
    body {
      font-family: -apple-system, "Helvetica Neue", Arial, sans-serif;
      background: #f5f5f3;
      min-height: 100vh;
      padding: 2rem 1rem;
      color: #1a1a1a;
    }
    .container { max-width: 480px; margin: 0 auto; display: flex; flex-direction: column; gap: 12px; }

    .card {
      background: #fff;
      border-radius: 20px;
      padding: 1.5rem;
      border: 1px solid #e8e8e4;
    }

    /* 目前天氣 */
    .city { font-size: 14px; color: #888; margin-bottom: 4px; }
    .main-temp { display: flex; align-items: center; gap: 12px; margin-bottom: 4px; }
    .icon { font-size: 44px; line-height: 1; }
    .temp { font-size: 60px; font-weight: 300; letter-spacing: -2px; }
    .temp sup { font-size: 22px; font-weight: 400; vertical-align: super; }
    .description { font-size: 15px; color: #555; margin-bottom: 1rem; }
    .meta { display: flex; gap: 1.5rem; font-size: 13px; color: #888; padding-top: 1rem; border-top: 1px solid #f0f0ec; }
    .meta strong { color: #333; font-weight: 500; }

    /* 每小時區塊 */
    .section-title { font-size: 13px; color: #888; font-weight: 500; margin-bottom: 1rem; }

    /* 橫向捲動小時列 */
    .hour-scroll { display: flex; gap: 8px; overflow-x: auto; padding-bottom: 6px; scrollbar-width: none; }
    .hour-scroll::-webkit-scrollbar { display: none; }
    .hour-item {
      flex-shrink: 0;
      display: flex; flex-direction: column; align-items: center; gap: 4px;
      padding: 10px 10px;
      border-radius: 12px;
      border: 1px solid #f0f0ec;
      min-width: 56px;
    }
    .hour-item.now { background: #1a1a1a; border-color: #1a1a1a; }
    .hour-item.now .hour-label,
    .hour-item.now .hour-temp { color: #fff; }
    .hour-label { font-size: 11px; color: #aaa; }
    .hour-icon { font-size: 18px; }
    .hour-temp { font-size: 14px; font-weight: 500; color: #1a1a1a; }
    .hour-rain { font-size: 10px; color: #5b9bd5; }

    /* 折線圖 */
    .chart-wrap { position: relative; height: 160px; margin-top: 4px; }

    /* 5天預報 */
    .forecast-row {
      display: flex; align-items: center; justify-content: space-between;
      padding: 9px 0; border-bottom: 1px solid #f5f5f3;
      font-size: 14px;
    }
    .forecast-row:last-child { border-bottom: none; }
    .forecast-day { width: 40px; color: #888; }
    .forecast-icon { font-size: 18px; }
    .forecast-rain { color: #5b9bd5; font-size: 12px; width: 36px; text-align: center; }
    .forecast-temps .low { color: #aaa; margin-left: 6px; }

    .footer { text-align: center; font-size: 11px; color: #ccc; padding: 0.5rem 0; }
  </style>
</head>
<body>
<div class="container">

  <!-- 目前天氣 -->
  <div class="card">
    <p class="city">📍 {{ weather.city }}</p>
    <div class="main-temp">
      <span class="icon">{{ weather.icon }}</span>
      <span class="temp">{{ weather.temp }}<sup>°C</sup></span>
    </div>
    <p class="description">{{ weather.description }}</p>
    <div class="meta">
      <span>💧 濕度 <strong>{{ weather.humidity }}%</strong></span>
      <span>💨 風速 <strong>{{ weather.wind }} km/h</strong></span>
    </div>
  </div>

  <!-- 每小時 -->
  <div class="card">
    <p class="section-title">今天每小時</p>

    <div class="hour-scroll">
      {% set now_hour = now_hour %}
      {% for h in weather.hours %}
      <div class="hour-item {% if loop.index0 == current_hour_index %}now{% endif %}">
        <span class="hour-label">{{ h.hour }}</span>
        <span class="hour-icon">{{ h.icon }}</span>
        <span class="hour-temp">{{ h.temp }}°</span>
        <span class="hour-rain">{{ h.rain }}%</span>
      </div>
      {% endfor %}
    </div>

    <!-- 折線圖 -->
    <div class="chart-wrap">
      <canvas id="tempChart"></canvas>
    </div>
  </div>

  <!-- 5天預報 -->
  <div class="card">
    <p class="section-title">5 天預報</p>
    <div class="forecast">
      {% for day in weather.forecast %}
      <div class="forecast-row">
        <span class="forecast-day">{{ day.day }}</span>
        <span class="forecast-icon">{{ day.icon }}</span>
        <span class="forecast-rain">{{ day.rain }}%</span>
        <span class="forecast-temps">
          <strong>{{ day.high }}°</strong>
          <span class="low">{{ day.low }}°</span>
        </span>
      </div>
      {% endfor %}
    </div>
  </div>

  <p class="footer">資料來源：Open-Meteo（免費，無需 API key）</p>
</div>

<script>
  const labels = {{ weather.hours | map(attribute='hour') | list | tojson }};
  const temps  = {{ weather.hours | map(attribute='temp') | list | tojson }};

  const ctx = document.getElementById('tempChart').getContext('2d');
  new Chart(ctx, {
    type: 'line',
    data: {
      labels: labels,
      datasets: [{
        data: temps,
        borderColor: '#1a1a1a',
        borderWidth: 1.5,
        pointRadius: 3,
        pointBackgroundColor: '#1a1a1a',
        tension: 0.4,
        fill: true,
        backgroundColor: 'rgba(26,26,26,0.04)'
      }]
    },
    options: {
      responsive: true,
      maintainAspectRatio: false,
      plugins: { legend: { display: false }, tooltip: {
        callbacks: { label: ctx => ctx.parsed.y + '°C' }
      }},
      scales: {
        x: { grid: { display: false }, ticks: { font: { size: 10 }, color: '#aaa',
          callback: function(val, i) { return i % 3 === 0 ? this.getLabelForValue(val) : ''; }
        }},
        y: { grid: { color: '#f5f5f3' }, ticks: { font: { size: 10 }, color: '#aaa',
          callback: v => v + '°' }}
      }
    }
  });
</script>
</body>
</html>

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Multi Timezone Digital Clock</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin:0;
      font-family: Arial, sans-serif;
      background: linear-gradient(135deg,#ff512f,#dd2476);
      color: #fff;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .clock-container {
      background: rgba(0,0,0,0.6);
      padding: 24px 32px;
      border-radius: 20px;
      box-shadow: 0 6px 32px #0005;
      max-width: 350px;
    }
    h2 {
      margin-top: 0;
      padding-bottom: 10px;
      text-align: center;
      font-size: 24px;
    }
    .time-zones {
      display: flex;
      flex-direction: column;
      gap: 16px;
    }
    .zone {
      display: flex;
      justify-content: space-between;
      font-size: 22px;
      background: #fff1;
      padding: 10px 18px;
      border-radius: 10px;
      align-items: center;
    }
    .zone span.label {
      font-weight: bold;
      font-size: 1em;
      letter-spacing: 1px;
      min-width: 120px;
    }
    .zone span.time {
      font-family: "Consolas", monospace;
      letter-spacing: 2px;
      font-size: 1.1em;
      min-width: 120px;
      text-align: right;
      color: #00e676;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div class="clock-container">
    <h2>Digital Clock<br> (Multiple Time Zones)</h2>
    <div class="time-zones" id="zones">
      <!-- Time zones will be rendered here -->
    </div>
  </div>
  <script>
    // Edit or add zones as needed
    const timeZoneList = [
      { label: "Local Time", timeZone: undefined },
      { label: "India (IST)", timeZone: "Asia/Kolkata" },
      { label: "London (GMT/UK)", timeZone: "Europe/London" },
      { label: "New York (EST)", timeZone: "America/New_York" },
      { label: "Tokyo (JST)", timeZone: "Asia/Tokyo" },
      { label: "Sydney (AEST)", timeZone: "Australia/Sydney" }
    ];

    function renderZones() {
      const zonesDiv = document.getElementById('zones');
      zonesDiv.innerHTML = "";
      for (const [i, zone] of timeZoneList.entries()) {
        const div = document.createElement('div');
        div.className = 'zone';
        div.innerHTML = `<span class="label">${zone.label}</span><span class="time" id="clock${i}">--:--:--</span>`;
        zonesDiv.appendChild(div);
      }
    }

    function updateClocks() {
      timeZoneList.forEach((zone, i) => {
        const span = document.getElementById('clock' + i);
        const now = new Date();
        let options = {
          hour: '2-digit',
          minute: '2-digit',
          second: '2-digit',
        };
        if(zone.timeZone) {
          options.timeZone = zone.timeZone;
        }
        const timeStr = now.toLocaleTimeString([], options);
        span.textContent = timeStr;
      });
    }

    renderZones();
    updateClocks();
    setInterval(updateClocks, 1000);
  </script>
</body>
</html>

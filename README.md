<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Prop Firm Brokers</title>
  <style>
    body { font-family: Arial, sans-serif; background: #f4f4f9; padding: 20px; }
    h1 { text-align: center; }
    .container { display: grid; grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); gap: 20px; }
    .card { background: white; border-radius: 12px; padding: 20px; box-shadow: 0 4px 6px rgba(0,0,0,0.1); text-align: center; }
    .card img { width: 120px; height: auto; margin-bottom: 15px; }
    .card h2 { font-size: 20px; margin-bottom: 10px; }
    .card p { font-size: 14px; color: #555; margin-bottom: 15px; }
    .card button { background: #007BFF; color: white; border: none; padding: 10px 15px; border-radius: 8px; cursor: pointer; }
    .card button:hover { background: #0056b3; }
  </style>
</head>
<body>
  <h1>Top Prop Firm Brokers</h1>
  <div class="container" id="brokers"></div>

  <script>
    async function loadBrokers() {
      const res = await fetch("http://localhost:5000/api/firms");
      const brokers = await res.json();
      const container = document.getElementById("brokers");
      brokers.forEach(broker => {
        container.innerHTML += `
          <div class="card">
            <img src="${broker.logo}" alt="${broker.name} Logo">
            <h2>${broker.name}</h2>
            <p>${broker.description}</p>
            <button onclick="window.open('${broker.affiliate_link}', '_blank')">Visit Broker</button>
          </div>
        `;
      });
    }
    loadBrokers();
  </script>
</body>
</html>

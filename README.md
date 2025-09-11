<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Prop Firm Brokers</title>
  <style>
    body { font-family: Arial, sans-serif; padding: 20px; background: #f9f9f9; }
    .container { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 20px; }
    .card { background: white; padding: 15px; border-radius: 12px; box-shadow: 0 4px 10px rgba(0,0,0,0.1); text-align: center; }
    .card img { max-width: 100px; margin-bottom: 10px; }
    .card h3 { margin: 10px 0; }
    .card p { font-size: 14px; color: #555; }
    .card a { display: inline-block; margin-top: 10px; padding: 8px 12px; background: #007BFF; color: white; text-decoration: none; border-radius: 6px; }
    .card a:hover { background: #0056b3; }
  </style>
</head>
<body>
  <h1>Prop Firm Brokers</h1>
  <div class="container" id="brokers"></div>

  <script>
    async function loadBrokers() {
      const res = await fetch("http://localhost:5000/api/firms");
      const brokers = await res.json();
      const container = document.getElementById("brokers");

      brokers.forEach(broker => {
        const card = document.createElement("div");
        card.className = "card";
        card.innerHTML = `
          <img src="${broker.logo}" alt="${broker.name}">
          <h3>${broker.name}</h3>
          <p>${broker.description}</p>
          <p><strong>Profit Split:</strong> ${broker.profit_split}</p>
          <a href="${broker.affiliate_link}" target="_blank">Visit Broker</a>
        `;
        container.appendChild(card);
      });
    }
    loadBrokers();
  </script>
</body>
</html>

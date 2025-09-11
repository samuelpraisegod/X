<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prop Firm Brokers</title>
    <style>
        body { font-family: Arial, sans-serif; background-color: #f4f4f4; padding: 20px; }
        .container { display: flex; flex-wrap: wrap; justify-content: center; }
        .card { background: white; border: 1px solid #ddd; border-radius: 8px; padding: 15px; margin: 10px; width: 300px; box-shadow: 0 2px 5px rgba(0,0,0,0.1); text-align: center; }
        .card img { max-width: 100px; height: auto; margin-bottom: 10px; }
        .card h2 { font-size: 1.5em; margin: 10px 0; }
        .card p { font-size: 0.9em; color: #555; }
        .card button { background: #007bff; color: white; border: none; padding: 10px 20px; border-radius: 5px; cursor: pointer; }
        .card button:hover { background: #0056b3; }
    </style>
</head>
<body>
    <h1>Prop Firm Brokers</h1>
    <div class="container" id="firms-container"></div>

    <script>
        fetch('http://localhost:3000/api/firms') // Change to your hosted API URL later
            .then(response => response.json())
            .then(data => {
                const container = document.getElementById('firms-container');
                data.forEach(firm => {
                    const card = document.createElement('div');
                    card.className = 'card';
                    card.innerHTML = `
                        <img src="${firm.logo}" alt="${firm.name} Logo">
                        <h2>${firm.name}</h2>
                        <p>${firm.description}</p>
                        <p>Profit Split: ${firm.profit_split}</p>
                        <a href="${firm.affiliate_link}" target="_blank" rel="noopener noreferrer">
                            <button>Visit Broker</button>
                        </a>
                    `;
                    container.appendChild(card);
                });
            })
            .catch(error => console.error('Error fetching firms:', error));
    </script>
</body>
</html>

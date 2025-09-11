<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prop Firm Brokers Demo - 2025 Edition</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            background-color: #f4f4f4; 
            padding: 20px; 
            margin: 0;
        }
        h1, h2 { text-align: center; color: #333; }
        .section { margin: 40px 0; padding: 20px; background: white; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); }
        .container { 
            display: flex; 
            flex-wrap: wrap; 
            justify-content: center; 
            gap: 20px;
            max-width: 1200px;
            margin: 0 auto;
        }
        .card { 
            background: white; 
            border: 1px solid #ddd; 
            border-radius: 12px; 
            padding: 20px; 
            width: 300px; 
            box-shadow: 0 4px 8px rgba(0,0,0,0.1); 
            text-align: center; 
            transition: transform 0.2s;
        }
        .card:hover { transform: translateY(-5px); }
        .card img { 
            max-width: 100px; 
            height: auto; 
            margin-bottom: 15px; 
            border-radius: 50%;
        }
        .card h2 { 
            font-size: 1.4em; 
            margin: 10px 0; 
            color: #007bff;
        }
        .card p { 
            font-size: 0.9em; 
            color: #555; 
            line-height: 1.4;
        }
        .profit-split {
            background: #e7f3ff;
            padding: 8px;
            border-radius: 5px;
            font-weight: bold;
            color: #0056b3;
        }
        .card button { 
            background: #28a745; 
            color: white; 
            border: none; 
            padding: 12px 24px; 
            border-radius: 6px; 
            cursor: pointer; 
            font-size: 1em;
            width: 100%;
            margin-top: 10px;
        }
        .card button:hover { 
            background: #218838; 
        }
        /* New Table Styles */
        .table-container { overflow-x: auto; }
        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th, td { padding: 12px; text-align: left; border-bottom: 1px solid #ddd; }
        th { background: #f8f9fa; font-weight: bold; color: #333; }
        tr:hover { background: #f5f5f5; }
        .promo { background: #d4edda; padding: 4px 8px; border-radius: 4px; font-size: 0.85em; }
        .action-btn { background: #007bff; color: white; border: none; padding: 8px 16px; border-radius: 4px; cursor: pointer; text-decoration: none; display: inline-block; }
        .action-btn:hover { background: #0056b3; }
        @media (max-width: 600px) {
            .container { flex-direction: column; align-items: center; }
            th, td { padding: 8px 4px; font-size: 0.9em; }
        }
    </style>
</head>
<body>
    <h1>Top Prop Firm Brokers - September 2025 Demo</h1>
    <p style="text-align: center; color: #666;">Updated with the latest firms based on recent reviews. Click "Visit Broker" to explore (affiliate links ready for commissions).</p>

    <!-- Cards Section (Existing) -->
    <div class="container" id="firms-container"></div>

    <!-- Placeholder for Create Co-Funding Section -->
    <section id="create-co-funding" class="section">
        <h2>Create Co-Funding</h2>
        <p>Start your co-funding journey here. Fill out the form to get matched with partners.</p>
        <button style="background: #28a745; color: white; border: none; padding: 12px 24px; border-radius: 6px; cursor: pointer;">Create New Co-Funding</button>
    </section>

    <!-- New Prop Firms Table Section -->
    <section id="prop-firms-table" class="section">
        <h2>Prop Firms Overview</h2>
        <p>Compare top prop firms with key metrics. (Static for demo; will fetch from API later.)</p>
        <div class="table-container">
            <table>
                <thead>
                    <tr>
                        <th>Firm</th>
                        <th>Rank / Reviews</th>
                        <th>Country</th>
                        <th>Years in Operation</th>
                        <th>Assets</th>
                        <th>Platforms</th>
                        <th>Max Allocations</th>
                        <th>Promo</th>
                        <th>Profit Split</th>
                        <th>Action</th>
                    </tr>
                </thead>
                <tbody id="table-body">
                    <!-- Static row populated by JS below -->
                </tbody>
            </table>
        </div>
    </section>

    <script>
        // Existing Cards Data and Render (unchanged)
        const firms = [
            {
                name: 'FTMO',
                website: 'https://ftmo.com/',
                description: 'Leading prop firm for forex traders with two-phase challenges, scaling up to $2M, and support for MT4/MT5/cTrader platforms.',
                profit_split: 'Up to 90%',
                logo: 'https://ftmo.com/wp-content/themes/ftmo/assets/images/ftmo-logo-white.svg',
                affiliate_link: 'https://ftmo.com/en/affiliate-program/?ref=yourid'
            },
            // ... (other firms as before; truncated for brevity)
            {
                name: 'FundedNext',
                website: 'https://fundednext.com/',
                description: 'Flexible forex and futures prop firm with no time limits, scaling to $4M, fast payouts, and MT5/cTrader support.',
                profit_split: 'Up to 95%',
                logo: 'https://fundednext.com/assets/images/fundednext-logo.png',
                affiliate_link: 'https://fundednext.com/affiliate?ref=yourid'
            }
            // Add back the full list if needed
        ];

        // Render cards
        const container = document.getElementById('firms-container');
        firms.forEach(firm => {
            const card = document.createElement('div');
            card.className = 'card';
            card.innerHTML = `
                <img src="${firm.logo}" alt="${firm.name} Logo" onerror="this.src='https://via.placeholder.com/100x100/CCCCCC/FFFFFF?text=${firm.name.charAt(0)}';">
                <h2>${firm.name}</h2>
                <p>${firm.description}</p>
                <div class="profit-split">Profit Split: ${firm.profit_split}</div>
                <a href="${firm.affiliate_link}" target="_blank" rel="noopener noreferrer">
                    <button>Visit Broker</button>
                </a>
            `;
            container.appendChild(card);
        });

        // New: Static Table Data (expand to array for multiple rows; fetch from API later)
        const firmsTableData = [
            {
                firm: 'FTMO',
                rankReviews: '1 / 4.8 (25K+)',
                country: 'Czech Republic',
                years: '10',
                assets: 'Forex, Indices, Commodities, Crypto',
                platforms: 'MT4, MT5, cTrader',
                maxAllocations: '$2,000,000',
                promo: '25% Off Challenges',
                profitSplit: 'Up to 90%',
                affiliateLink: 'https://ftmo.com/en/affiliate-program/?ref=yourid'
            }
            // Add more rows here, e.g., FundedNext: { firm: 'FundedNext', rankReviews: '2 / 4.7 (15K+)', ... }
        ];

        // Render Table Rows
        const tableBody = document.getElementById('table-body');
        firmsTableData.forEach(row => {
            const tr = document.createElement('tr');
            tr.innerHTML = `
                <td>${row.firm}</td>
                <td>${row.rankReviews}</td>
                <td>${row.country}</td>
                <td>${row.years}</td>
                <td>${row.assets}</td>
                <td>${row.platforms}</td>
                <td>${row.maxAllocations}</td>
                <td><span class="promo">${row.promo}</span></td>
                <td>${row.profitSplit}</td>
                <td><a href="${row.affiliateLink}" target="_blank" rel="noopener noreferrer" class="action-btn">View Details</a></td>
            `;
            tableBody.appendChild(tr);
        });

        // Future: To make dynamic, replace above with:
        // fetch('http://localhost:3000/api/firms').then(res => res.json()).then(data => { /* map and render */ });
    </script>
</body>
</html>

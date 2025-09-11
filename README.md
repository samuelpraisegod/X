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
        h1 { text-align: center; color: #333; }
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
        #create-co-funding {
            max-width: 1200px;
            margin: 40px auto;
            padding: 20px;
            background: white;
            border-radius: 12px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
            text-align: center;
        }
        #create-co-funding h2 {
            color: #333;
            margin-bottom: 10px;
        }
        #prop-firms-table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        #prop-firms-table th,
        #prop-firms-table td {
            padding: 12px;
            text-align: left;
            border-bottom: 1px solid #ddd;
        }
        #prop-firms-table th {
            background: #f8f9fa;
            font-weight: bold;
            color: #333;
        }
        #prop-firms-table tr:hover {
            background: #f5f5f5;
        }
        #prop-firms-table tr:nth-child(even) {
            background: #f9f9f9;
        }
        .action-btn {
            background: #007bff;
            color: white;
            border: none;
            padding: 8px 16px;
            border-radius: 4px;
            cursor: pointer;
            text-decoration: none;
            display: inline-block;
        }
        .action-btn:hover {
            background: #0056b3;
        }
        .promo {
            font-weight: bold;
            color: #28a745;
        }
        @media (max-width: 768px) {
            .container { flex-direction: column; align-items: center; }
            #prop-firms-table {
                font-size: 0.9em;
            }
            #prop-firms-table th,
            #prop-firms-table td {
                padding: 8px;
            }
        }
    </style>
</head>
<body>
    <h1>Top Prop Firm Brokers - September 2025 Demo</h1>
    <p style="text-align: center; color: #666;">Updated with the latest firms based on recent reviews. Click "Visit Broker" to explore (affiliate links ready for commissions).</p>
    
    <!-- Original Cards Section -->
    <div class="container" id="firms-container"></div>

    <!-- Placeholder for "Create Co-Funding" Section -->
    <section id="create-co-funding">
        <h2>Create Co-Funding</h2>
        <p>Here you can set up co-funding opportunities with partners. (Placeholder for your actual form/button.)</p>
    </section>

    <!-- New Prop Firms Table Section -->
    <section style="max-width: 1200px; margin: 40px auto;">
        <h2 style="text-align: center; color: #333;">Prop Firms Comparison Table</h2>
        <table id="prop-firms-table">
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
            <tbody>
                <!-- Static Example Row for FTMO -->
                <tr>
                    <td>FTMO</td>
                    <td>#1 / 4.8/5 (20k+ reviews)</td>
                    <td>Czech Republic</td>
                    <td>9</td>
                    <td>Forex, Indices, Crypto, Metals</td>
                    <td>MT4, MT5, cTrader</td>
                    <td>$2M</td>
                    <td class="promo">25% off with PROPFIRMS25</td>
                    <td>80-90%</td>
                    <td><a href="https://ftmo.com/en/affiliate-program/?ref=yourid" target="_blank" rel="noopener noreferrer" class="action-btn">Visit Broker</a></td>
                </tr>
                <!-- Add more rows dynamically later via JS/API -->
            </tbody>
        </table>
        <p style="text-align: center; color: #666; margin-top: 10px;">(Static demo row. Will fetch from API for full data.)</p>
    </section>

    <script>
        // Simulated API data (from previous demo)
        const firms = [
            {
                name: 'FTMO',
                website: 'https://ftmo.com/',
                description: 'Leading prop firm for forex traders with two-phase challenges, scaling up to $2M, and support for MT4/MT5/cTrader platforms.',
                profit_split: 'Up to 90%',
                logo: 'https://ftmo.com/wp-content/themes/ftmo/assets/images/ftmo-logo-white.svg',
                affiliate_link: 'https://ftmo.com/en/affiliate-program/?ref=yourid'
            },
            // ... (other firms from previous)
            {
                name: 'FundedNext',
                website: 'https://fundednext.com/',
                description: 'Flexible forex and futures prop firm with no time limits, scaling to $4M, fast payouts, and MT5/cTrader support.',
                profit_split: 'Up to 95%',
                logo: 'https://fundednext.com/assets/images/fundednext-logo.png',
                affiliate_link: 'https://fundednext.com/affiliate?ref=yourid'
            },
            {
                name: 'The5%ers',
                website: 'https://the5ers.com/',
                description: 'Forex-focused firm with instant funding options, high-profit shares, and programs for scalpers to swing traders on MT5.',
                profit_split: 'Up to 100%',
                logo: 'https://the5ers.com/wp-content/uploads/2023/05/the5ers-logo-white.png',
                affiliate_link: 'https://the5ers.com/affiliate-program/?ref=yourid'
            },
            {
                name: 'DNA Funded',
                website: 'https://dnafunded.com/',
                description: 'Top-rated 2025 firm by CBS News, US-friendly with low fees, customizable challenges, and access to 800+ markets via ASIC-regulated broker.',
                profit_split: '80-90%',
                logo: 'https://via.placeholder.com/100x100/4A90E2/FFFFFF?text=DNA',
                affiliate_link: 'https://dnafunded.com/affiliate?ref=yourid'
            },
            {
                name: 'FXIFY',
                website: 'https://fxify.com/',
                description: 'Multi-asset prop firm with instant payouts after first trade, EA support, scaling to $400K, and beginner-friendly evaluations.',
                profit_split: 'Up to 90%',
                logo: 'https://fxify.com/assets/images/fxify-logo.svg',
                affiliate_link: 'https://fxify.com/affiliate?ref=yourid'
            },
            {
                name: 'Topstep',
                website: 'https://topstep.com/',
                description: 'Futures prop firm with one-step evaluation, no time limits, free coaching, and high initial profit keeps for US traders.',
                profit_split: '100% on first $10K, then 90%',
                logo: 'https://www.topstep.com/hubfs/Topstep_Logo_White.png',
                affiliate_link: 'https://topstep.com/affiliate?ref=yourid'
            },
            {
                name: 'Apex Trader Funding',
                website: 'https://apextraderfunding.com/',
                description: 'Streamlined futures firm with relaxed rules, high capital up to $300K, and support for NinjaTrader/TradingView.',
                profit_split: '100% on first $25K, then 90%',
                logo: 'https://apextraderfunding.com/wp-content/uploads/2023/04/apex-logo-white.png',
                affiliate_link: 'https://apextraderfunding.com/affiliate?ref=yourid'
            },
            {
                name: 'BrightFunded',
                website: 'https://brightfunded.com/',
                description: 'Multi-asset firm with unlimited scaling, weekly payouts, two-phase challenges, and desktop/mobile platforms.',
                profit_split: '80-100%',
                logo: 'https://brightfunded.com/wp-content/uploads/2023/10/brightfunded-logo.png',
                affiliate_link: 'https://brightfunded.com/affiliate?ref=yourid'
            },
            {
                name: 'Funder Trading',
                website: 'https://fundertrading.com/',
                description: 'Top for options and stocks in 2025, with coaching for beginners, up to $500K buying power, and no other assets.',
                profit_split: 'Up to 90%',
                logo: 'https://via.placeholder.com/100x100/FF6B35/FFFFFF?text=Funder',
                affiliate_link: 'https://fundertrading.com/affiliate?ref=yourid'
            },
            {
                name: 'For Traders',
                website: 'https://fortraders.com/',
                description: 'Beginner-friendly global firm with $5M+ payouts, 25K+ traders, MT5/cTrader/TradeLocker, and flexible styles.',
                profit_split: 'Up to 90%',
                logo: 'https://via.placeholder.com/100x100/00C851/FFFFFF?text=FT',
                affiliate_link: 'https://fortraders.com/affiliate?ref=yourid'
            }
        ];

        // Render cards (simulates API fetch for cards)
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

        // Future: Dynamic table population (uncomment and adapt when API ready)
        /*
        fetch('http://localhost:3000/api/firms')
            .then(response => response.json())
            .then(data => {
                const tbody = document.querySelector('#prop-firms-table tbody');
                tbody.innerHTML = ''; // Clear static row
                data.forEach(firm => {
                    const row = document.createElement('tr');
                    row.innerHTML = `
                        <td>${firm.name}</td>
                        <td>${firm.rank} / ${firm.reviews}</td>
                        <td>${firm.country}</td>
                        <td>${firm.years}</td>
                        <td>${firm.assets}</td>
                        <td>${firm.platforms}</td>
                        <td>${firm.max_allocation}</td>
                        <td class="promo">${firm.promo || 'None'}</td>
                        <td>${firm.profit_split}</td>
                        <td><a href="${firm.affiliate_link}" target="_blank" rel="noopener noreferrer" class="action-btn">Visit Broker</a></td>
                    `;
                    tbody.appendChild(row);
                });
            });
        */
    </script>
</body>
</html>

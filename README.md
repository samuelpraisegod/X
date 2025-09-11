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
        @media (max-width: 600px) {
            .container { flex-direction: column; align-items: center; }
        }
    </style>
</head>
<body>
    <h1>Top Prop Firm Brokers - September 2025 Demo</h1>
    <p style="text-align: center; color: #666;">Updated with the latest firms based on recent reviews. Click "Visit Broker" to explore (affiliate links ready for commissions).</p>
    <div class="container" id="firms-container"></div>

    <script>
        // Simulated API data (updated for 2025 from Benzinga, CBS News, etc.)
        const firms = [
            {
                name: 'FTMO',
                website: 'https://ftmo.com/',
                description: 'Leading prop firm for forex traders with two-phase challenges, scaling up to $2M, and support for MT4/MT5/cTrader platforms.',
                profit_split: 'Up to 90%',
                logo: 'https://ftmo.com/wp-content/themes/ftmo/assets/images/ftmo-logo-white.svg',
                affiliate_link: 'https://ftmo.com/en/affiliate-program/?ref=yourid'
            },
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

        // Render cards (simulates API fetch)
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
    </script>
</body>
</html>

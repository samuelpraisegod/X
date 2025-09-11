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
            color: #333;
        }
        h1 { 
            text-align: center; 
            color: #007bff; 
            margin-bottom: 30px;
        }
        .container { 
            display: flex; 
            flex-wrap: wrap; 
            justify-content: center; 
            gap: 20px;
        }
        .card { 
            background: white; 
            border: 1px solid #ddd; 
            border-radius: 12px; 
            padding: 20px; 
            width: 320px; 
            box-shadow: 0 4px 8px rgba(0,0,0,0.1); 
            text-align: center; 
            transition: transform 0.2s;
        }
        .card:hover { 
            transform: translateY(-5px);
        }
        .card img { 
            max-width: 120px; 
            height: auto; 
            margin-bottom: 15px; 
            border-radius: 8px;
        }
        .card h2 { 
            font-size: 1.6em; 
            margin: 10px 0; 
            color: #007bff;
        }
        .card p { 
            font-size: 0.95em; 
            color: #555; 
            line-height: 1.4;
        }
        .profit { 
            font-weight: bold; 
            color: #28a745; 
            font-size: 1.1em;
        }
        .card button { 
            background: #007bff; 
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
            background: #0056b3; 
        }
        .footer {
            text-align: center;
            margin-top: 40px;
            font-size: 0.9em;
            color: #777;
        }
    </style>
</head>
<body>
    <h1>Top Prop Firm Brokers - 2025 Demo</h1>
    <div class="container" id="firms-container"></div>
    <div class="footer">
        <p>Demo powered by Grok | Updated Sep 2025 | <a href="#" style="color: #007bff;">Add Filters Later</a></p>
    </div>

    <script>
        // Simulated API data (updated for 2025 from recent sources)
        const firmsData = [
            {
                name: 'FTMO',
                website: 'https://ftmo.com/',
                description: 'Leading prop firm funding up to $400K (scaling to $2M) with rigorous evaluations, MT4/MT5 support, and global trader community.',
                profit_split: '80-90%',
                logo: 'https://ftmo.com/wp-content/themes/ftmo/assets/images/ftmo-logo-white.svg',
                affiliate_link: 'https://ftmo.com/en/affiliate-program/?ref=yourid'
            },
            {
                name: 'FundedNext',
                website: 'https://fundednext.com/',
                description: 'Flexible funding up to $4M with no time limits, MT5/cTrader platforms, and instant payouts for forex/futures traders.',
                profit_split: 'Up to 95%',
                logo: 'https://fundednext.com/assets/images/fundednext-logo.png',
                affiliate_link: 'https://fundednext.com/affiliate?ref=yourid'
            },
            {
                name: 'The5%ers',
                website: 'https://the5ers.com/',
                description: 'Forex-focused with instant funding options, MT5 support, scaling to $4M, and high-profit shares for all levels.',
                profit_split: 'Up to 100%',
                logo: 'https://the5ers.com/wp-content/uploads/2023/05/the5ers-logo-white.png',
                affiliate_link: 'https://the5ers.com/affiliate-program/?ref=yourid'
            },
            {
                name: 'DNA Funded',
                website: 'https://dnafunded.com/',
                description: 'US-friendly with low fees, over 800 markets, customizable challenges, and broker-backed reliability.',
                profit_split: '80-90%',
                logo: 'https://dnafunded.com/wp-content/uploads/2024/01/logo.png',
                affiliate_link: 'https://dnafunded.com/affiliate?ref=yourid'
            },
            {
                name: 'BrightFunded',
                website: 'https://brightfunded.com/',
                description: 'Multi-asset firm with unlimited scaling, weekly payouts, Trade2Earn loyalty, and up to 100% splits.',
                profit_split: '80-100%',
                logo: 'https://brightfunded.com/wp-content/uploads/2023/10/brightfunded-logo.png',
                affiliate_link: 'https://brightfunded.com/affiliate-program?ref=yourid'
            },
            {
                name: 'FXIFY',
                website: 'https://fxify.com/',
                description: 'Fast payouts after first trade, EA support, scaling to $400K, and customizable add-ons for experienced traders.',
                profit_split: 'Up to 90%',
                logo: 'https://fxify.com/assets/images/fxify-logo.svg',
                affiliate_link: 'https://fxify.com/affiliate?ref=yourid'
            },
            {
                name: 'Topstep',
                website: 'https://topstep.com/',
                description: 'Futures-focused with one-step eval, no time limits, CME access via NinjaTrader/TradingView, and strong scaling.',
                profit_split: '100% first $10K, then 90%',
                logo: 'https://www.topstep.com/hubfs/Topstep_Logo_White.png',
                affiliate_link: 'https://topstep.com/affiliate?ref=yourid'
            },
            {
                name: 'Apex Trader Funding',
                website: 'https://apextraderfunding.com/',
                description: 'Relaxed rules for futures, up to $300K accounts, no daily drawdowns, and high initial profit keeps.',
                profit_split: '100% first $25K, then 90%',
                logo: 'https://apextraderfunding.com/wp-content/uploads/2023/04/apex-logo-white.png',
                affiliate_link: 'https://apextraderfunding.com/affiliate?ref=yourid'
            },
            {
                name: 'Funded Trading Plus',
                website: 'https://fundedtradingplus.com/',
                description: 'Advanced scaling to $2.5M, instant funding options, and flexible rules for stocks/forex.',
                profit_split: '80-100%',
                logo: 'https://fundedtradingplus.com/wp-content/uploads/2023/05/FTP-Logo.png',
                affiliate_link: 'https://fundedtradingplus.com/affiliate?ref=yourid'
            },
            {
                name: 'Take Profit Trader',
                website: 'https://takeprofittrader.com/',
                description: 'Futures prop with immediate withdrawals, consistency rules, and accounts up to $150K on multiple platforms.',
                profit_split: '80-90%',
                logo: 'https://takeprofittrader.com/wp-content/uploads/2023/06/tpt-logo.png',
                affiliate_link: 'https://takeprofittrader.com/affiliate?ref=yourid'
            }
        ];

        // Render cards
        const container = document.getElementById('firms-container');
        firmsData.forEach(firm => {
            const card = document.createElement('div');
            card.className = 'card';
            card.innerHTML = `
                <img src="${firm.logo}" alt="${firm.name} Logo" onerror="this.src='https://via.placeholder.com/120x80?text=${firm.name}'">
                <h2>${firm.name}</h2>
                <p>${firm.description}</p>
                <p class="profit">Profit Split: ${firm.profit_split}</p>
                <a href="${firm.affiliate_link}" target="_blank" rel="noopener noreferrer">
                    <button>Visit Broker (Affiliate)</button>
                </a>
                <p style="font-size: 0.8em; color: #888; margin-top: 10px;"><a href="${firm.website}" target="_blank">Official Site</a></p>
            `;
            container.appendChild(card);
        });
    </script>
</body>
</html>

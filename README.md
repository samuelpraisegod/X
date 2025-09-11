<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prop Firm Brokers Demo - September 2025</title>
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
        }
        .card { 
            background: white; 
            border: 1px solid #ddd; 
            border-radius: 8px; 
            padding: 15px; 
            width: 300px; 
            box-shadow: 0 2px 5px rgba(0,0,0,0.1); 
            text-align: center; 
            transition: transform 0.2s;
        }
        .card:hover { transform: scale(1.02); }
        .card img { 
            max-width: 100px; 
            height: auto; 
            margin-bottom: 10px; 
            border-radius: 50%;
        }
        .card h2 { 
            font-size: 1.5em; 
            margin: 10px 0; 
            color: #007bff;
        }
        .card p { 
            font-size: 0.9em; 
            color: #555; 
            line-height: 1.4;
        }
        .card .profit { 
            font-weight: bold; 
            color: #28a745;
        }
        .card button { 
            background: #007bff; 
            color: white; 
            border: none; 
            padding: 10px 20px; 
            border-radius: 5px; 
            cursor: pointer; 
            width: 100%;
            margin-top: 10px;
            text-decoration: none;
            display: block;
        }
        .card button:hover { 
            background: #0056b3; 
        }
        @media (max-width: 600px) { .card { width: 90%; } }
    </style>
</head>
<body>
    <h1>Prop Firm Brokers - Top Picks for September 2025</h1>
    <p style="text-align: center; color: #666;">Discover funded trading opportunities. All "Visit Broker" buttons use your affiliate links for commissions.</p>
    <div class="container" id="firms-container"></div>

    <script>
        const firms = [
            {
                name: 'FTMO',
                website: 'https://ftmo.com/',
                description: 'Leading prop firm for forex traders with challenges, scaling up to $2M, and support for MT4/MT5 platforms. Over $5M in payouts in 2025.',
                profit_split: '80-90%',
                logo: 'https://ftmo.com/wp-content/themes/ftmo/assets/images/ftmo-logo-white.svg',
                affiliate_link: 'https://ftmo.com/en/affiliate-program/?ref=yourid'
            },
            {
                name: 'FundedNext',
                website: 'https://fundednext.com/',
                description: 'Flexible prop firm for forex and futures with no time limits, scaling to $4M, and fast payouts. Top-rated for global reach.',
                profit_split: 'Up to 100%',
                logo: 'https://fundednext.com/assets/images/fundednext-logo.png',
                affiliate_link: 'https://fundednext.com/affiliate?ref=yourid'
            },
            {
                name: 'The 5%ers',
                website: 'https://the5ers.com/',
                description: 'Forex-focused prop firm with instant funding options, MT5 support, and high-profit shares for experienced traders. Ideal for beginners.',
                profit_split: 'Up to 100%',
                logo: 'https://the5ers.com/wp-content/uploads/2023/05/the5ers-logo-white.png',
                affiliate_link: 'https://the5ers.com/affiliate-program/?ref=yourid'
            },
            {
                name: 'DNA Funded',
                website: 'https://dnafunded.com/',
                description: 'Top-rated for 2025 by CBS News. US-friendly with low fees, customizable challenges, and access to over 800 markets including forex and indices.',
                profit_split: '80-90%',
                logo: 'https://via.placeholder.com/100?text=DNA+Funded',
                affiliate_link: 'https://example.com/dnafunded-affiliate?ref=yourid'
            },
            {
                name: 'BrightFunded',
                website: 'https://brightfunded.com/',
                description: 'Multi-asset prop firm with unlimited scaling, weekly payouts, and trader-focused programs. Supports cTrader and proprietary platforms.',
                profit_split: '80-100%',
                logo: 'https://brightfunded.com/wp-content/uploads/2023/10/brightfunded-logo.png',
                affiliate_link: 'https://example.com/brightfunded-affiliate?ref=yourid'
            },
            {
                name: 'FXIFY',
                website: 'https://fxify.com/',
                description: 'Prop firm for experienced traders with instant payouts, EA support, and scaling up to $400K. Winner of FTA25 Best Broker-Backed Firm.',
                profit_split: 'Up to 90%',
                logo: 'https://fxify.com/assets/images/fxify-logo.svg',
                affiliate_link: 'https://example.com/fxify-affiliate?ref=yourid'
            },
            {
                name: 'Topstep',
                website: 'https://topstep.com/',
                description: 'Leading futures prop firm with one-step evaluation, no time limits, and high initial profit keeps. Access to 32 futures markets.',
                profit_split: '100% on first $10K, then 90%',
                logo: 'https://www.topstep.com/hubfs/Topstep_Logo_White.png',
                affiliate_link: 'https://topstep.com/affiliate?ref=yourid'
            },
            {
                name: 'City Traders Imperium',
                website: 'https://citytradersimperium.com/',
                description: 'High-profit split prop firm with salary programs, scaling, and support for beginners. US-friendly with MT5/Match-Trader.',
                profit_split: '80-100%',
                logo: 'https://citytradersimperium.com/wp-content/uploads/2023/03/CTI-Logo-White.png',
                affiliate_link: 'https://citytradersimperium.com/affiliate?ref=yourid'
            },
            {
                name: 'Apex Trader Funding',
                website: 'https://apextraderfunding.com/',
                description: 'Streamlined futures prop firm with relaxed rules and high capital access up to $300K. Record $2.5M single payout in 2025.',
                profit_split: '100% on first $25K, then 90%',
                logo: 'https://apextraderfunding.com/wp-content/uploads/2023/04/apex-logo-white.png',
                affiliate_link: 'https://example.com/apex-affiliate?ref=yourid'
            },
            {
                name: 'Goat Funded Trader',
                website: 'https://goatfundedtrader.com/',
                description: 'Best for monthly salary options in forex/futures. Supports 61K+ traders across 180 countries with flexible challenges.',
                profit_split: 'Up to 100%',
                logo: 'https://via.placeholder.com/100?text=Goat+Funded',
                affiliate_link: 'https://example.com/goatfunded-affiliate?ref=yourid'
            }
        ];

        const container = document.getElementById('firms-container');
        firms.forEach(firm => {
            const card = document.createElement('div');
            card.className = 'card';
            card.innerHTML = `
                <img src="${firm.logo}" alt="${firm.name} Logo" onerror="this.src='https://via.placeholder.com/100?text=${firm.name}'">
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

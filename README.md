<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prop Firm Challenges - 2025 Demo</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            background-color: #1a1a1a; 
            color: #fff; 
            padding: 20px; 
            margin: 0;
        }
        h2 { text-align: center; color: #fff; }
        .section { margin: 40px 0; padding: 20px; background: white; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.2); max-width: 1200px; margin-left: auto; margin-right: auto; }
        /* Menu Tabs */
        .tabs { display: flex; justify-content: center; gap: 10px; margin-bottom: 20px; }
        .tab { 
            padding: 10px 20px; 
            cursor: pointer; 
            background: #333; 
            border-radius: 6px 6px 0 0; 
            font-weight: bold; 
            color: #fff; 
            transition: background 0.2s;
        }
        .tab.active { background: white; border-bottom: 2px solid #9b59b6; color: #9b59b6; }
        .tab:hover { background: #444; }
        .tab-content { display: none; }
        .tab-content.active { display: block; }
        /* Filter Bar (Challenges) */
        .filter-bar { display: flex; flex-wrap: wrap; gap: 10px; justify-content: space-between; align-items: center; margin-bottom: 20px; }
        .filter-bar select, .filter-bar input, .filter-bar button { 
            padding: 8px; 
            border: 1px solid #555; 
            border-radius: 4px; 
            font-size: 0.9em; 
            background: #2a2a2a; 
            color: #fff;
        }
        .filter-bar button { background: #9b59b6; cursor: pointer; }
        .filter-bar button:hover { background: #8e44ad; }
        .filter-bar .toggle { display: flex; align-items: center; gap: 5px; }
        .filter-bar input[type="checkbox"] { 
            appearance: none; 
            width: 40px; 
            height: 20px; 
            background: #555; 
            border-radius: 10px; 
            position: relative; 
            cursor: pointer;
        }
        .filter-bar input[type="checkbox"]:checked { background: #ff4d4d; }
        .filter-bar input[type="checkbox"]::before { 
            content: ''; 
            position: absolute; 
            width: 16px; 
            height: 16px; 
            background: white; 
            border-radius: 50%; 
            top: 2px; 
            left: 2px; 
            transition: 0.2s;
        }
        .filter-bar input[type="checkbox"]:checked::before { left: 22px; }
        .filter-bar input[type="text"] { width: 200px; }
        .filter-bar .circle-btn { border-radius: 50%; width: 40px; height: 40px; padding: 0; display: flex; align-items: center; justify-content: center; }
        .filter-bar .bookmark-btn { font-size: 1.2em; }
        /* Counts */
        .counts { text-align: center; margin: 10px 0; font-size: 1em; color: #fff; font-weight: bold; }
        /* Challenges Table */
        .challenges-table { width: 100%; border-collapse: collapse; }
        .challenges-table th, .challenges-table td { padding: 12px; text-align: left; border-bottom: 1px solid #444; }
        .challenges-table th { background: #2a2a2a; color: #fff; font-weight: bold; }
        .challenges-table tr:hover { background: #333; }
        .challenge-row { display: flex; align-items: center; }
        .challenge-row img { max-width: 50px; height: auto; border-radius: 50%; margin-right: 10px; }
        .challenge-row .firm-name { font-weight: bold; color: #fff; }
        .challenge-row .rating { 
            background: #6f42c1; 
            color: white; 
            padding: 4px 8px; 
            border-radius: 4px; 
            font-size: 0.85em; 
            margin-top: 5px;
        }
        .challenge-row .stars { color: #ffc107; }
        .challenge-row .bookmark { cursor: pointer; color: #9b59b6; font-size: 1.2em; margin-left: 10px; }
        .buy-btn { 
            background: linear-gradient(to right, #ff4d4d, #ff8c8c); 
            color: white; 
            border: none; 
            padding: 8px 16px; 
            border-radius: 20px; 
            cursor: pointer; 
            text-decoration: none; 
            display: inline-block;
        }
        .buy-btn:hover { background: linear-gradient(to right, #e63e3e, #ff6b6b); }
        .old-price { text-decoration: line-through; color: #999; font-size: 0.9em; margin-right: 5px; }
        /* Firms Table */
        .table-container { overflow-x: auto; }
        .firms-table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        .firms-table th, .firms-table td { padding: 12px; text-align: left; border-bottom: 1px solid #444; }
        .firms-table th { background: #2a2a2a; font-weight: bold; color: #fff; }
        .firms-table tr:hover { background: #333; }
        .promo { background: #d4edda; padding: 4px 8px; border-radius: 4px; font-size: 0.85em; color: #333; }
        .action-btn { 
            background: #9b59b6; 
            color: white; 
            border: none; 
            padding: 8px 16px; 
            border-radius: 4px; 
            cursor: pointer; 
            text-decoration: none; 
            display: inline-block; 
        }
        .action-btn:hover { background: #8e44ad; }
        .firm-name { 
            color: #9b59b6; 
            cursor: pointer; 
            text-decoration: underline; 
        }
        .firm-name:hover { color: #8e44ad; }
        .firm-details { 
            display: none; 
            padding: 15px; 
            background: #2a2a2a; 
            border: 1px solid #444; 
            border-radius: 8px; 
            margin: 10px 0; 
            text-align: center;
        }
        .firm-details.active { display: block; }
        .firm-details img { max-width: 100px; height: auto; border-radius: 50%; margin-bottom: 10px; }
        .firm-details h3 { font-size: 1.4em; color: #9b59b6; margin: 10px 0; }
        .firm-details p { font-size: 0.9em; color: #ccc; line-height: 1.4; }
        .firm-details button { 
            background: #ff4d4d; 
            color: white; 
            border: none; 
            padding: 12px 24px; 
            border-radius: 6px; 
            cursor: pointer; 
            font-size: 1em;
            margin-top: 10px;
        }
        .firm-details button:hover { background: #e63e3e; }
        @media (max-width: 600px) {
            .tabs { flex-direction: column; align-items: center; }
            .filter-bar { flex-direction: column; }
            .filter-bar input[type="text"] { width: 100%; }
            .challenges-table th, .challenges-table td, .firms-table th, .firms-table td { padding: 8px 4px; font-size: 0.85em; }
            .firm-details { padding: 10px; }
        }
    </style>
</head>
<body>
    <!-- Menu Tabs -->
    <div class="tabs">
        <div class="tab" data-tab="firms">Firms</div>
        <div class="tab active" data-tab="challenges">Challenges</div>
        <div class="tab" data-tab="offers">Offers</div>
        <div class="tab" data-tab="reviews">Reviews</div>
    </div>

    <!-- Tab Content -->
    <div id="firms" class="tab-content section">
        <h2>Prop Firms Overview</h2>
        <p>Compare top prop firms. Click the firm name for more details. (Static for demo; will fetch from API later.)</p>
        <div class="table-container">
            <table class="firms-table">
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
                <tbody id="firms-table-body">
                    <!-- Static row populated by JS -->
                </tbody>
            </table>
        </div>
    </div>
    <div id="challenges" class="tab-content section active">
        <h2>Trading Challenges</h2>
        <p>Explore available challenges from top prop firms. (Static for demo; will fetch from /api/challenges later.)</p>
        <div class="filter-bar">
            <button>Filter 🕳️</button>
            <select>
                <option value="FX">FX</option>
                <option value="Crypto">Crypto</option>
                <option value="Indices">Indices</option>
                <option value="Commodities">Commodities</option>
            </select>
            <select>
                <option value="100K">$100K</option>
                <option value="10K">$10K</option>
                <option value="50K">$50K</option>
                <option value="200K">$200K</option>
            </select>
            <select>
                <option value="2">2 Steps</option>
                <option value="1">1 Step</option>
            </select>
            <div class="toggle">
                <label>Apply Discount</label>
                <input type="checkbox">
            </div>
            <button class="circle-btn">All</button>
            <button class="bookmark-btn">🔖</button>
            <input type="text" placeholder="Search for Challenges">
        </div>
        <div class="table-container">
            <table class="challenges-table">
                <thead>
                    <tr>
                        <th>Firm / Rank</th>
                        <th>Account Size</th>
                        <th>Steps</th>
                        <th>Profit Target</th>
                        <th>Daily Loss</th>
                        <th>Max Loss</th>
                        <th>Profit Split</th>
                        <th>PA</th>
                        <th>Price</th>
                    </tr>
                </thead>
                <tbody id="challenges-table-body">
                    <!-- Static rows populated by JS -->
                </tbody>
            </table>
        </div>
    </div>
    <div id="offers" class="tab-content section">
        <h2>Special Offers</h2>
        <p>Discover the latest offers from prop firms. (Placeholder for future content.)</p>
    </div>
    <div id="reviews" class="tab-content section">
        <h2>Reviews</h2>
        <p>Read user reviews for prop firms. (Placeholder for future content.)</p>
    </div>

    <!-- Total Counts -->
    <div class="counts">
        Total Challenges: 2 | Total Firms: 1
    </div>

    <script>
        // Static Firms Data (FTMO from provided code)
        const firmsTableData = [
            {
                id: 1,
                firm: 'FTMO',
                rankReviews: '1 / 4.8 (25K+)',
                country: 'Czech Republic',
                years: '10',
                assets: 'Forex, Indices, Commodities, Crypto',
                platforms: 'MT4, MT5, cTrader',
                maxAllocations: '$2,000,000',
                promo: '25% Off Challenges',
                profitSplit: 'Up to 90%',
                affiliateLink: 'https://ftmo.com/en/affiliate-program/?ref=yourid',
                description: 'Leading prop firm for forex traders with two-phase challenges, scaling up to $2M, and support for MT4/MT5/cTrader platforms.',
                logo: 'https://ftmo.com/wp-content/themes/ftmo/assets/images/ftmo-logo-white.svg'
            }
        ];

        // Render Firms Table
        const firmsTableBody = document.getElementById('firms-table-body');
        firmsTableData.forEach(row => {
            const tr = document.createElement('tr');
            tr.innerHTML = `
                <td><span class="firm-name" data-firm-id="${row.id}">${row.firm}</span></td>
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
            firmsTableBody.appendChild(tr);

            // Add hidden details row
            const detailsRow = document.createElement('tr');
            detailsRow.innerHTML = `
                <td colspan="10">
                    <div class="firm-details" id="details-${row.id}">
                        <img src="${row.logo}" alt="${row.firm} Logo" onerror="this.src='https://via.placeholder.com/100x100/CCCCCC/FFFFFF?text=${row.firm.charAt(0)}';">
                        <h3>${row.firm}</h3>
                        <p>${row.description}</p>
                        <p><strong>Profit Split:</strong> ${row.profitSplit}</p>
                        <a href="${row.affiliateLink}" target="_blank" rel="noopener noreferrer">
                            <button>Visit Broker</button>
                        </a>
                    </div>
                </td>
            `;
            firmsTableBody.appendChild(tr);
        });

        // Static Challenges Data (FundingPips, The5ers)
        const challengesData = [
            {
                id: 1,
                firm: 'FundingPips',
                logo: 'https://fundingpips.com/wp-content/uploads/2023/04/fundingpips-logo.png',
                rating: '4.7',
                reviews: '12K+',
                accountSize: '$100K',
                steps: '2 Steps',
                profitTarget: '6% / 6%',
                dailyLoss: '3%',
                maxLoss: '6%',
                profitSplit: '80%',
                pa: 'Standard',
                price: '$379.05',
                oldPrice: '$399.00',
                affiliateLink: 'https://fundingpips.com/affiliate?ref=yourid'
            },
            {
                id: 2,
                firm: 'The5ers',
                logo: 'https://the5ers.com/wp-content/uploads/2023/05/the5ers-logo-white.png',
                rating: '4.8',
                reviews: '15K+',
                accountSize: '$100K',
                steps: '2 Steps',
                profitTarget: '10% / 5%',
                dailyLoss: '4%',
                maxLoss: '8%',
                profitSplit: 'Up to 100%',
                pa: 'Instant Funding',
                price: '$495.00',
                oldPrice: '$520.00',
                affiliateLink: 'https://the5ers.com/affiliate-program/?ref=yourid'
            }
        ];

        // Render Challenges Table
        const challengesTableBody = document.getElementById('challenges-table-body');
        challengesData.forEach(row => {
            const tr = document.createElement('tr');
            tr.innerHTML = `
                <td class="challenge-row">
                    <img src="${row.logo}" alt="${row.firm} Logo" onerror="this.src='https://via.placeholder.com/50x50/CCCCCC/FFFFFF?text=${row.firm.charAt(0)}';">
                    <div>
                        <div class="firm-name">${row.firm}</div>
                        <div class="rating"><span class="stars">★★★★★</span> ${row.rating} (${row.reviews})</div>
                    </div>
                    <span class="bookmark">🔖</span>
                </td>
                <td>${row.accountSize}</td>
                <td>${row.steps}</td>
                <td>${row.profitTarget}</td>
                <td>${row.dailyLoss}</td>
                <td>${row.maxLoss}</td>
                <td>${row.profitSplit}</td>
                <td>${row.pa}</td>
                <td>
                    <span class="old-price">${row.oldPrice}</span>
                    ${row.price}
                    <br>
                    <a href="${row.affiliateLink}" target="_blank" rel="noopener noreferrer" class="buy-btn">Buy Now</a>
                </td>
            `;
            challengesTableBody.appendChild(tr);
        });

        // Toggle Firm Details on Click
        document.querySelectorAll('.firm-name').forEach(firm => {
            firm.addEventListener('click', () => {
                const firmId = firm.getAttribute('data-firm-id');
                const details = document.getElementById(`details-${firmId}`);
                if (details) details.classList.toggle('active');
            });
        });

        // Tab Switching
        document.querySelectorAll('.tab').forEach(tab => {
            tab.addEventListener('click', () => {
                document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
                document.querySelectorAll('.tab-content').forEach(c => c.classList.remove('active'));
                tab.classList.add('active');
                document.getElementById(tab.getAttribute('data-tab')).classList.add('active');
            });
        });

        // Bookmark Icon (Placeholder)
        document.querySelectorAll('.bookmark').forEach(bookmark => {
            bookmark.addEventListener('click', () => {
                alert('Bookmark functionality to be implemented!');
            });
        });
    </script>
</body>
</html>

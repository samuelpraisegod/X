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
            color: #ccc; 
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
            border: 1px solid #444; 
            border-radius: 4px; 
            font-size: 0.9em; 
            background: #333; 
            color: #fff;
        }
        .filter-bar select:focus, .filter-bar input:focus { outline: none; border-color: #9b59b6; }
        .filter-bar button { background: #9b59b6; cursor: pointer; }
        .filter-bar button:hover { background: #8e44ad; }
        .filter-bar .filter-btn::before { content: '⚙️'; margin-right: 5px; }
        .filter-bar .all-btn { border-radius: 50%; width: 40px; height: 40px; display: flex; align-items: center; justify-content: center; }
        .filter-bar .bookmark-btn::before { content: '🔖'; }
        .filter-bar .toggle { display: flex; align-items: center; gap: 5px; }
        .filter-bar input[type="checkbox"] { 
            appearance: none; 
            width: 40px; 
            height: 20px; 
            background: #444; 
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
            transition: transform 0.2s;
        }
        .filter-bar input[type="checkbox"]:checked::before { transform: translateX(20px); }
        .filter-bar input[type="text"] { width: 200px; background: #333; }
        /* Challenges Table */
        .challenges-table { width: 100%; border-collapse: collapse; }
        .challenges-table th, .challenges-table td { padding: 12px; text-align: left; border-bottom: 1px solid #444; }
        .challenges-table th { background: #2c2c2c; font-weight: bold; color: #fff; }
        .challenges-table tr:hover { background: #2a2a2a; }
        .challenge-row { display: flex; align-items: center; justify-content: space-between; }
        .challenge-left { flex: 0 0 200px; display: flex; flex-direction: column; align-items: flex-start; }
        .challenge-left img { max-width: 60px; height: auto; border-radius: 50%; margin-bottom: 5px; }
        .challenge-left h3 { font-size: 1.2em; margin: 5px 0; color: #fff; }
        .challenge-left .rating { background: #6f42c1; color: white; padding: 4px 8px; border-radius: 4px; font-size: 0.85em; }
        .challenge-left .stars { color: #ffc107; }
        .challenge-left .bookmark { cursor: pointer; color: #9b59b6; font-size: 1.2em; }
        .challenge-middle { flex: 1; display: flex; justify-content: space-around; }
        .challenge-middle div { flex: 1; text-align: center; }
        .challenge-right { flex: 0 0 200px; text-align: right; }
        .challenge-right .price { font-size: 1.1em; font-weight: bold; color: #fff; }
        .challenge-right .old-price { text-decoration: line-through; color: #888; font-size: 0.9em; }
        .challenge-right .buy-btn { 
            background: linear-gradient(to right, #ff4d4d, #ff8c8c); 
            color: white; 
            border: none; 
            padding: 8px 16px; 
            border-radius: 20px; 
            cursor: pointer; 
            margin-top: 5px; 
            display: inline-block; 
            text-decoration: none;
        }
        .challenge-right .buy-btn:hover { background: linear-gradient(to right, #e63e3e, #ff6b6b); }
        /* Counts */
        .counts { text-align: center; margin: 10px 0; font-size: 1em; color: #fff; font-weight: bold; }
        @media (max-width: 600px) {
            .tabs { flex-direction: column; align-items: center; }
            .filter-bar { flex-direction: column; }
            .filter-bar input[type="text"] { width: 100%; }
            .challenges-table th, .challenges-table td { padding: 8px 4px; font-size: 0.85em; }
            .challenge-row { flex-direction: column; align-items: flex-start; }
            .challenge-right { text-align: left; margin-top: 10px; }
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
        <p>Compare top prop firms. (Placeholder; will fetch from /api/firms.)</p>
    </div>
    <div id="challenges" class="tab-content section active">
        <h2>Challenges</h2>
        <p>Explore trading challenges from top prop firms. (Static for demo; will fetch from /api/challenges.)</p>
        <div class="filter-bar">
            <button class="filter-btn">Filter</button>
            <select>
                <option value="">Assets</option>
                <option value="FX">FX</option>
                <option value="Crypto">Crypto</option>
                <option value="Indices">Indices</option>
                <option value="Commodities">Commodities</option>
            </select>
            <select>
                <option value="">Size</option>
                <option value="10K">$10K</option>
                <option value="50K">$50K</option>
                <option value="100K">$100K</option>
                <option value="200K">$200K</option>
            </select>
            <select>
                <option value="">Steps</option>
                <option value="1">1 Step</option>
                <option value="2">2 Steps</option>
            </select>
            <div class="toggle">
                <label>Apply Discount</label>
                <input type="checkbox">
            </div>
            <button class="all-btn">All</button>
            <button class="bookmark-btn"></button>
            <input type="text" placeholder="Search for Challenges">
        </div>
        <div class="challenges-table">
            <div class="challenge-row" style="background: #2c2c2c; font-weight: bold;">
                <div class="challenge-left">Firm / Rank</div>
                <div class="challenge-middle">
                    <div>Account Size</div>
                    <div>Steps</div>
                    <div>Profit Target</div>
                    <div>Daily Loss</div>
                    <div>Max Loss</div>
                    <div>Profit Split</div>
                    <div>PA</div>
                </div>
                <div class="challenge-right">Price</div>
            </div>
            <!-- Static rows populated by JS below -->
            <div id="challenges-body"></div>
        </div>
    </div>
    <div id="offers" class="tab-content section">
        <h2>Offers</h2>
        <p>Discover special offers from prop firms. (Placeholder for future content.)</p>
    </div>
    <div id="reviews" class="tab-content section">
        <h2>Reviews</h2>
        <p>Read user reviews for prop firms. (Placeholder for future content.)</p>
    </div>

    <!-- Total Counts -->
    <div class="counts">
        Total Challenges: 2 | Total Firms: 0
    </div>

    <script>
        // Static Challenges Data (FundingPips, The5%ers)
        const challengesData = [
            {
                id: 1,
                firm: 'FundingPips',
                logo: 'https://via.placeholder.com/60x60/CCCCCC/FFFFFF?text=FP',
                rating: '4.7',
                reviews: '18K+',
                accountSize: '$100K',
                steps: '2 Steps',
                profitTarget: '6% / 6%',
                dailyLoss: '3%',
                maxLoss: '6%',
                profitSplit: '80%',
                pa: 'MT5',
                price: '$379.05',
                oldPrice: '$399.00',
                affiliateLink: 'https://fundingpips.com/affiliate?ref=yourid'
            },
            {
                id: 2,
                firm: 'The5%ers',
                logo: 'https://the5ers.com/wp-content/uploads/2023/05/the5ers-logo-white.png',
                rating: '4.8',
                reviews: '12K+',
                accountSize: '$100K',
                steps: '2 Steps',
                profitTarget: '10% / 5%',
                dailyLoss: '5%',
                maxLoss: '10%',
                profitSplit: '100%',
                pa: 'MT5',
                price: '$495.00',
                oldPrice: '$525.00',
                affiliateLink: 'https://the5ers.com/affiliate-program/?ref=yourid'
            }
        ];

        // Render Challenges Table Rows
        const challengesBody = document.getElementById('challenges-body');
        challengesData.forEach(challenge => {
            const row = document.createElement('div');
            row.className = 'challenge-row';
            row.innerHTML = `
                <div class="challenge-left">
                    <img src="${challenge.logo}" alt="${challenge.firm} Logo" onerror="this.src='https://via.placeholder.com/60x60/CCCCCC/FFFFFF?text=${challenge.firm.charAt(0)}';">
                    <h3>${challenge.firm}</h3>
                    <div class="rating"><span class="stars">★★★★★</span> ${challenge.rating} (${challenge.reviews})</div>
                    <span class="bookmark">🔖</span>
                </div>
                <div class="challenge-middle">
                    <div>${challenge.accountSize}</div>
                    <div>${challenge.steps}</div>
                    <div>${challenge.profitTarget}</div>
                    <div>${challenge.dailyLoss}</div>
                    <div>${challenge.maxLoss}</div>
                    <div>${challenge.profitSplit}</div>
                    <div>${challenge.pa}</div>
                </div>
                <div class="challenge-right">
                    <div class="price">${challenge.price} <span class="old-price">${challenge.oldPrice}</span></div>
                    <a href="${challenge.affiliateLink}" target="_blank" rel="noopener noreferrer" class="buy-btn">Buy Now</a>
                </div>
            `;
            challengesBody.appendChild(row);
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

        // Bookmark (Placeholder)
        document.querySelectorAll('.bookmark').forEach(bookmark => {
            bookmark.addEventListener('click', () => {
                alert('Bookmark functionality to be implemented!');
            });
        });
    </script>
</body>
</html>

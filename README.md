<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Prop Firm Brokers - 2025 Demo</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            background-color: #1a1a1a; 
            color: #e0e0e0; 
            padding: 20px; 
            margin: 0;
        }
        h2 { text-align: center; color: #e0e0e0; }
        .section { margin: 40px 0; padding: 20px; background: #2a2a2a; border-radius: 12px; box-shadow: 0 4px 8px rgba(0,0,0,0.2); max-width: 1200px; margin-left: auto; margin-right: auto; }
        /* Menu Tabs */
        .tabs { display: flex; justify-content: center; gap: 10px; margin-bottom: 20px; }
        .tab { 
            padding: 10px 20px; 
            cursor: pointer; 
            background: #333; 
            border-radius: 6px 6px 0 0; 
            font-weight: bold; 
            color: #e0e0e0; 
            transition: background 0.2s;
        }
        .tab.active { background: white; color: #6f42c1; border-bottom: 2px solid #ff4d4d; }
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
            color: #e0e0e0;
        }
        .filter-bar button { background: #6f42c1; cursor: pointer; }
        .filter-bar button:hover { background: #5a32a3; }
        .filter-bar button.all-btn { border-radius: 50%; width: 40px; height: 40px; }
        .filter-bar button.bookmark-btn { font-size: 1.2em; }
        .filter-bar .toggle { display: flex; align-items: center; gap: 5px; }
        .filter-bar input[type="checkbox"] { width: auto; accent-color: #ff4d4d; }
        .filter-bar input[type="text"] { width: 200px; }
        /* Filter Bar (Firms, Offers) */
        .other-filter-bar { display: flex; flex-wrap: wrap; gap: 10px; justify-content: center; align-items: center; margin-bottom: 20px; }
        .other-filter-bar button { background: #6f42c1; color: #e0e0e0; }
        .other-filter-bar button.active { background: #ff4d4d; }
        .other-filter-bar button:hover { background: #5a32a3; }
        .other-filter-bar input[type="text"] { width: 200px; }
        /* Counts */
        .counts { text-align: center; margin: 10px 0; font-size: 1em; color: #e0e0e0; font-weight: bold; }
        /* Table Styles (Firms) */
        .table-container { overflow-x: auto; }
        table { width: 100%; border-collapse: collapse; margin-top: 10px; }
        th, td { padding: 12px; text-align: left; border-bottom: 1px solid #444; }
        th { background: #333; font-weight: bold; color: #e0e0e0; }
        tr:hover { background: #2f2f2f; }
        .promo { background: #d4edda; padding: 4px 8px; border-radius: 4px; font-size: 0.85em; color: #333; }
        .action-btn { 
            background: #6f42c1; 
            color: white; 
            border: none; 
            padding: 8px 16px; 
            border-radius: 4px; 
            cursor: pointer; 
            text-decoration: none; 
            display: inline-block; 
        }
        .action-btn:hover { background: #5a32a3; }
        /* Firm Column Clickable */
        .firm-name { 
            color: #ff4d4d; 
            cursor: pointer; 
            text-decoration: underline; 
        }
        .firm-name:hover { color: #e63e3e; }
        .firm-details { 
            display: none; 
            padding: 15px; 
            background: #333; 
            border: 1px solid #444; 
            border-radius: 8px; 
            margin: 10px 0; 
            text-align: center;
        }
        .firm-details.active { display: block; }
        .firm-details img { 
            max-width: 100px; 
            height: auto; 
            border-radius: 50%; 
            margin-bottom: 10px;
        }
        .firm-details h3 { 
            font-size: 1.4em; 
            color: #ff4d4d; 
            margin: 10px 0;
        }
        .firm-details p { 
            font-size: 0.9em; 
            color: #e0e0e0; 
            line-height: 1.4;
        }
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
        /* Challenges Table */
        .challenges-table { width: 100%; border-collapse: collapse; }
        .challenges-table th, .challenges-table td { padding: 12px; border-bottom: 1px solid #444; }
        .challenges-table th { background: #333; }
        .challenges-table .firm-info { display: flex; align-items: center; gap: 10px; }
        .challenges-table img { max-width: 50px; height: auto; border-radius: 50%; }
        .challenges-table .firm-name { font-weight: bold; color: #e0e0e0; text-decoration: none; }
        .challenges-table .rating { background: #6f42c1; color: white; padding: 4px 8px; border-radius: 4px; font-size: 0.85em; }
        .challenges-table .stars { color: #ffc107; }
        .challenges-table .bookmark-icon { cursor: pointer; color: #ff4d4d; font-size: 1.2em; }
        .challenges-table .price { color: #e0e0e0; }
        .challenges-table .old-price { text-decoration: line-through; color: #888; margin-left: 5px; }
        .challenges-table .buy-btn { 
            background: linear-gradient(to right, #ff4d4d, #ff8c8c); 
            color: white; 
            border: none; 
            padding: 8px 16px; 
            border-radius: 20px; 
            cursor: pointer; 
            text-decoration: none;
        }
        .challenges-table .buy-btn:hover { background: linear-gradient(to right, #e63e3e, #ff6b6b); }
        /* Offer Card */
        .offer-card { 
            display: flex; 
            justify-content: space-between; 
            background: #2a2a2a; 
            border: 1px solid #444; 
            border-radius: 8px; 
            padding: 15px; 
            margin: 10px 0; 
            box-shadow: 0 2px 5px rgba(0,0,0,0.2); 
        }
        .offer-card-left { flex: 1; }
        .offer-card-right { 
            flex: 0 0 200px; 
            background: #333; 
            padding: 10px; 
            border-radius: 6px; 
            text-align: center; 
            margin-left: 10px;
        }
        .offer-card img { max-width: 80px; height: auto; border-radius: 50%; }
        .offer-card h3 { font-size: 1.3em; margin: 10px 0; color: #e0e0e0; }
        .offer-card .rating { color: white; background: #6f42c1; padding: 4px 8px; border-radius: 4px; font-size: 0.85em; }
        .offer-card .stars { color: #ffc107; }
        .offer-card .discount { font-weight: bold; color: #ff4d4d; font-size: 1.1em; }
        .offer-card .description { font-size: 0.9em; color: #e0e0e0; }
        .offer-card-bottom { 
            display: flex; 
            justify-content: space-between; 
            align-items: center; 
            margin-top: 10px; 
            border-top: 1px solid #444; 
            padding-top: 10px;
        }
        .offer-card .promo-code { font-size: 0.9em; font-weight: bold; color: #e0e0e0; }
        .offer-card .copy-icon { cursor: pointer; color: #ff4d4d; margin-left: 5px; }
        .offer-card .buy-btn { 
            background: linear-gradient(to right, #ff4d4d, #ff8c8c); 
            color: white; 
            border: none; 
            padding: 8px 16px; 
            border-radius: 6px; 
            cursor: pointer; 
            text-decoration: none;
        }
        .offer-card .buy-btn:hover { background: linear-gradient(to right, #e63e3e, #ff6b6b); }
        @media (max-width: 600px) {
            .tabs { flex-direction: column; align-items: center; }
            .filter-bar, .other-filter-bar { flex-direction: column; }
            .filter-bar input[type="text"] { width: 100%; }
            th, td { padding: 8px 4px; font-size: 0.85em; }
            .firm-details, .offer-card { flex-direction: column; }
            .offer-card-right { margin-left: 0; margin-top: 10px; }
            .challenges-table td { display: block; text-align: center; }
            .challenges-table .firm-info { justify-content: center; }
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
        <div class="other-filter-bar">
            <select>
                <option value="">Filter</option>
                <option value="profit_split">Profit Split</option>
                <option value="country">Country</option>
                <option value="years">Years in Operation</option>
            </select>
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
            <button>All</button>
            <button>Bookmarks</button>
            <input type="text" placeholder="Search for Challenges">
        </div>
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
    </div>
    <div id="challenges" class="tab-content section active">
        <h2>Challenges</h2>
        <p>Explore trading challenges from top prop firms. (Static for demo; will fetch from /api/challenges later.)</p>
        <div class="filter-bar">
            <button>🕳️ Filter</button>
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
                <tbody id="challenges-body">
                    <!-- Static rows populated by JS below -->
                </tbody>
            </table>
        </div>
    </div>
    <div id="offers" class="tab-content section">
        <h2>Special Offers</h2>
        <p>Discover the latest offers from top prop firms. (Static for demo; will fetch from /api/offers later.)</p>
        <div class="other-filter-bar">
            <button>September Offers 🔥</button>
            <button class="active">Exclusive Offers</button>
            <button>All Current Offers</button>
            <input type="text" placeholder="Search for Offers">
        </div>
        <div id="offers-container">
            <!-- Static offer card populated by JS below -->
        </div>
    </div>
    <div id="reviews" class="tab-content section">
        <h2>Reviews</h2>
        <p>Read user reviews for prop firms. (Placeholder for future content.)</p>
    </div>

    <!-- Total Counts -->
    <div class="counts">
        Total Challenges: 2 | Total Firms: 1 | Total Offers: 1
    </div>

    <script>
        // Static Firms Table Data (FTMO)
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

        // Render Firms Table Rows
        const tableBody = document.getElementById('table-body');
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
            tableBody.appendChild(tr);

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
            tableBody.appendChild(tr);
        });

        // Static

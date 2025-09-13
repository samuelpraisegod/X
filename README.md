<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pacific Prop Firm Co-Funding Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f4f4f4;
        }
        #main-content {
            max-width: 600px;
            margin: 20px auto;
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .toggle-container {
            display: flex;
            align-items: center;
            margin-bottom: 20px;
        }
        .toggle-container label {
            margin-right: 10px;
            font-weight: bold;
        }
        .toggle-switch {
            position: relative;
            display: inline-block;
            width: 60px;
            height: 34px;
        }
        .toggle-switch input {
            opacity: 0;
            width: 0;
            height: 0;
        }
        .slider {
            position: absolute;
            cursor: pointer;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-color: #ccc;
            transition: .4s;
            border-radius: 34px;
        }
        .slider:before {
            position: absolute;
            content: "";
            height: 26px;
            width: 26px;
            left: 4px;
            bottom: 4px;
            background-color: white;
            transition: .4s;
            border-radius: 50%;
        }
        input:checked + .slider {
            background-color: #2196F3;
        }
        input:checked + .slider:before {
            transform: translateX(26px);
        }
        form label {
            display: block;
            margin: 10px 0 5px;
        }
        form select, form button {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border-radius: 4px;
            border: 1px solid #ccc;
        }
        form button {
            background-color: #2196F3;
            color: white;
            border: none;
            cursor: pointer;
        }
        form button:disabled {
            background-color: #cccccc;
            cursor: not-allowed;
        }
        #contributionDetails {
            background: #f9f9f9;
            padding: 15px;
            border-radius: 4px;
            margin-top: 20px;
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
        }
        #contributionDetails .breakdown {
            flex: 1;
        }
        #buyButton {
            background-color: #28a745;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            color: white;
            cursor: pointer;
            margin-left: 20px;
        }
        #buyButton:disabled {
            background-color: #cccccc;
            cursor: not-allowed;
        }
        #result {
            color: green;
            margin-top: 10px;
        }
        .error {
            color: red;
        }
    </style>
</head>
<body>
    <div id="main-content">
        <h1>Pacific Prop Firm Co-Funding Calculator</h1>
        <div class="settings-section">
            <h2>Request Details</h2>
            <div class="toggle-container">
                <label for="calculatorToggle">Co-Funding:</label>
                <label class="toggle-switch">
                    <input type="checkbox" id="calculatorToggle" checked>
                    <span class="slider"></span>
                </label>
                <span id="toggleStatus">ON</span>
            </div>
            <form id="coFundingForm">
                <label for="propFirm">Prop Firm:</label>
                <select id="propFirm" name="propFirm" required>
                    <option value="">Select Prop Firm</option>
                    <option value="FTMO">FTMO</option>
                    <option value="E8 Funding">E8 Funding</option>
                    <option value="The5ers">The5ers</option>
                </select>

                <label for="accountSize">Account Size:</label>
                <select id="accountSize" name="accountSize" required>
                    <option value="">Select Account Size</option>
                </select>

                <label>Profit Split Agreement:</label>
                <p>70/30</p>

                <div id="contributionDetails">
                    <div class="breakdown">
                        <h3>showTab - Contribution Breakdown</h3>
                        <p><strong>Account Price:</strong> <span id="accountPrice">TBD</span></p>
                        <p><strong>Profit Split:</strong> <span id="selectedProfitSplit">70/30</span></p>
                        <p><strong>Requester Contribution:</strong> <span id="requesterContribution">TBD</span></p>
                        <p><strong>Partner Contribution:</strong> <span id="partnerContribution">TBD</span></p>
                    </div>
                    <button type="button" id="buyButton">Buy</button>
                </div>

                <button type="submit" id="submitButton">Submit Request</button>
                <p id="result"></p>
            </form>
        </div>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const form = document.getElementById('coFundingForm');
            const propFirm = document.getElementById('propFirm');
            const accountSize = document.getElementById('accountSize');
            const accountPrice = document.getElementById('accountPrice');
            const selectedProfitSplit = document.getElementById('selectedProfitSplit');
            const requesterContribution = document.getElementById('requesterContribution');
            const partnerContribution = document.getElementById('partnerContribution');
            const result = document.getElementById('result');
            const calculatorToggle = document.getElementById('calculatorToggle');
            const toggleStatus = document.getElementById('toggleStatus');
            const submitButton = document.getElementById('submitButton');
            const buyButton = document.getElementById('buyButton');
            const contributionDetails = document.getElementById('contributionDetails');

            // Simulated API data for prop firms (replace with actual API in production)
            // Prices based on 2025 offers, with $15 for $1K as per example
            const propFirmData = {
                'FTMO': {
                    accountSizes: [
                        { size: '10000', price: 170 }, // USD, ~155 EUR
                        { size: '25000', price: 275 }, // ~250 EUR
                        { size: '50000', price: 380 }, // ~345 EUR
                        { size: '100000', price: 594 } // ~540 EUR
                    ]
                },
                'E8 Funding': {
                    accountSizes: [
                        { size: '1000', price: 15 },   // As per example
                        { size: '5000', price: 59 },
                        { size: '10000', price: 99 },
                        { size: '25000', price: 208 },
                        { size: '50000', price: 338 }
                    ]
                },
                'The5ers': {
                    accountSizes: [
                        { size: '1000', price: 15 },   // As per example
                        { size: '5000', price: 39 },
                        { size: '10000', price: 85 },
                        { size: '25000', price: 165 },
                        { size: '50000', price: 260 }
                    ]
                }
            };

            // Simulate API call to fetch prop firm account sizes
            function fetchPropFirmDetails(firm) {
                // TODO: Replace with actual API call, e.g.:
                // return fetch(`/api/propfirm/details?firm=${firm}`)
                //   .then(response => response.json());
                return Promise.resolve(propFirmData[firm] || { accountSizes: [] });
            }

            // Simulate API call to fetch price for specific account size
            function getPrice(firm, size) {
                // TODO: Replace with actual API call, e.g.:
                // return fetch(`/api/propfirm/price?firm=${firm}&size=${size}`)
                //   .then(response => response.json())
                //   .then(data => data.price);
                const firmData = propFirmData[firm];
                const account = firmData?.accountSizes.find(acc => acc.size === size);
                return Promise.resolve(account?.price || 0);
            }

            // Populate account size dropdown
            function populateAccountSizes(firm) {
                accountSize.innerHTML = '<option value="">Select Account Size</option>';
                const firmData = propFirmData[firm];
                if (firmData && firmData.accountSizes) {
                    firmData.accountSizes.forEach(acc => {
                        const option = document.createElement('option');
                        option.value = acc.size;
                        option.textContent = `$${parseInt(acc.size).toLocaleString()}`;
                        accountSize.appendChild(option);
                    });
                }
            }

            // Update contributions
            async function updateContributions() {
                const firm = propFirm.value;
                const size = accountSize.value;
                const split = 70; // Fixed at 70/30 as per requirement

                let price = 0;
                if (firm && size) {
                    price = await getPrice(firm, size);
                }

                accountPrice.textContent = price ? `$${price.toFixed(2)}` : 'TBD';
                selectedProfitSplit.textContent = '70/30';
                
                if (price && split) {
                    const requesterShare = (price * split) / 100;
                    const partnerShare = price - requesterShare;
                    requesterContribution.textContent = `$${requesterShare.toFixed(2)}`;
                    partnerContribution.textContent = `$${partnerShare.toFixed(2)}`;
                } else {
                    requesterContribution.textContent = 'TBD';
                    partnerContribution.textContent = 'TBD';
                }
            }

            // Toggle co-funding functionality
            function toggleCoFunding() {
                const isEnabled = calculatorToggle.checked;
                toggleStatus.textContent = isEnabled ? 'ON' : 'OFF';
                propFirm.disabled = !isEnabled;
                accountSize.disabled = !isEnabled;
                submitButton.disabled = !isEnabled;
                buyButton.disabled = !isEnabled;
                contributionDetails.style.display = isEnabled ? 'flex' : 'none';
                if (isEnabled) {
                    updateContributions();
                } else {
                    accountPrice.textContent = 'TBD';
                    selectedProfitSplit.textContent = '70/30';
                    requesterContribution.textContent = 'TBD';
                    partnerContribution.textContent = 'TBD';
                    result.textContent = '';
                }
            }

            // Event listeners
            calculatorToggle.addEventListener('change', toggleCoFunding);
            propFirm.addEventListener('change', async () => {
                const firm = propFirm.value;
                if (firm) {
                    await fetchPropFirmDetails(firm);
                    populateAccountSizes(firm);
                    updateContributions();
                } else {
                    accountSize.innerHTML = '<option value="">Select Account Size</option>';
                    updateContributions();
                }
            });
            accountSize.addEventListener('change', updateContributions);

            // Form submission (Submit Request button)
            form.addEventListener('submit', async (e) => {
                e.preventDefault();

                if (!calculatorToggle.checked) {
                    result.textContent = 'Co-Funding is turned off. Please turn it on to submit.';
                    result.className = 'error';
                    return;
                }

                const firm = propFirm.value;
                const size = accountSize.value;

                if (firm && size) {
                    const price = await getPrice(firm, size);
                    const requesterShare = (price * 70) / 100; // Fixed 70/30 split
                    result.textContent = `Request submitted! Your contribution of $${requesterShare.toFixed(2)} is locked.`;
                    result.className = '';
                } else {
                    result.textContent = 'Please select a prop firm and account size.';
                    result.className = 'error';
                }
            });

            // Buy button (same action as submit)
            buyButton.addEventListener('click', async () => {
                if (!calculatorToggle.checked) {
                    result.textContent = 'Co-Funding is turned off. Please turn it on to buy.';
                    result.className = 'error';
                    return;
                }

                const firm = propFirm.value;
                const size = accountSize.value;

                if (firm && size) {
                    const price = await getPrice(firm, size);
                    const requesterShare = (price * 70) / 100; // Fixed 70/30 split
                    result.textContent = `Purchase confirmed! Your contribution of $${requesterShare.toFixed(2)} is locked.`;
                    result.className = '';
                } else {
                    result.textContent = 'Please select a prop firm and account size.';
                    result.className = 'error';
                }
            });

            // Initial setup
            toggleCoFunding();
            updateContributions();
        });
    </script>
</body>
</html>

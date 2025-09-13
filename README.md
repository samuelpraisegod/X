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
        #profitSplitTap {
            cursor: pointer;
            background-color: #e0e0e0;
            padding: 10px;
            border-radius: 4px;
            margin: 10px 0;
            font-weight: bold;
        }
        #profitSplitDetails {
            display: none;
            margin-left: 10px;
        }
        #contributionDetails {
            background: #f9f9f9;
            padding: 15px;
            border-radius: 4px;
            margin-top: 20px;
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
                <label for="accountSize">Account Size:</label>
                <select id="accountSize" name="accountSize" required>
                    <option value="">Select Account Size</option>
                    <option value="1000">$1,000</option>
                    <option value="5000">$5,000</option>
                    <option value="10000">$10,000</option>
                    <option value="25000">$25,000</option>
                    <option value="50000">$50,000</option>
                </select>

                <div id="profitSplitTap">Profit Split Agreement (Tap to View)</div>
                <div id="profitSplitDetails">
                    <p>70/30</p>
                </div>

                <div id="contributionDetails">
                    <h3>showTab - Contribution Breakdown</h3>
                    <p><strong>Account Price:</strong> <span id="accountPrice">TBD</span></p>
                    <p><strong>Profit Split:</strong> <span id="selectedProfitSplit">70/30</span></p>
                    <p><strong>Requester Contribution:</strong> <span id="requesterContribution">TBD</span></p>
                    <p><strong>Partner Contribution:</strong> <span id="partnerContribution">TBD</span></p>
                </div>

                <button type="submit" id="submitButton">Submit Request</button>
                <p id="result"></p>
            </form>
        </div>
    </div>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const form = document.getElementById('coFundingForm');
            const accountSize = document.getElementById('accountSize');
            const accountPrice = document.getElementById('accountPrice');
            const selectedProfitSplit = document.getElementById('selectedProfitSplit');
            const requesterContribution = document.getElementById('requesterContribution');
            const partnerContribution = document.getElementById('partnerContribution');
            const result = document.getElementById('result');
            const calculatorToggle = document.getElementById('calculatorToggle');
            const toggleStatus = document.getElementById('toggleStatus');
            const submitButton = document.getElementById('submitButton');
            const contributionDetails = document.getElementById('contributionDetails');
            const profitSplitTap = document.getElementById('profitSplitTap');
            const profitSplitDetails = document.getElementById('profitSplitDetails');

            // Simulated API data for account sizes and prices (replace with actual API)
            // Prices based on 2025 offers, with $15 for $1K as per example
            const accountData = {
                '1000': 15,   // As per example
                '5000': 39,   // Typical for $5K account
                '10000': 85,  // Typical for $10K
                '25000': 165, // Typical for $25K
                '50000': 260  // Typical for $50K
            };

            // Simulate API call to fetch price for account size
            function getPrice(size) {
                // TODO: Replace with actual API call, e.g.:
                // return fetch(`/api/propfirm/price?size=${size}`)
                //   .then(response => response.json())
                //   .then(data => data.price);
                return Promise.resolve(accountData[size] || 0);
            }

            // Update contributions
            async function updateContributions() {
                const size = accountSize.value;
                const split = 70; // Fixed at 70/30 as per requirement

                let price = 0;
                if (size) {
                    price = await getPrice(size);
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
                accountSize.disabled = !isEnabled;
                submitButton.disabled = !isEnabled;
                contributionDetails.style.display = isEnabled ? 'block' : 'none';
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

            // Toggle profit split details visibility
            profitSplitTap.addEventListener('click', () => {
                profitSplitDetails.style.display = profitSplitDetails.style.display === 'block' ? 'none' : 'block';
            });

            // Event listeners
            calculatorToggle.addEventListener('change', toggleCoFunding);
            accountSize.addEventListener('change', updateContributions);

            // Form submission
            form.addEventListener('submit', async (e) => {
                e.preventDefault();

                if (!calculatorToggle.checked) {
                    result.textContent = 'Co-Funding is turned off. Please turn it on to submit.';
                    result.className = 'error';
                    return;
                }

                const size = accountSize.value;

                if (size) {
                    const price = await getPrice(size);
                    const requesterShare = (price * 70) / 100; // Fixed 70/30 split
                    result.textContent = `Request submitted! Your contribution of $${requesterShare.toFixed(2)} is locked.`;
                    result.className = '';
                } else {
                    result.textContent = 'Please select an account size.';
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

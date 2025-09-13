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
        form button {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            border-radius: 4px;
            border: 1px solid #ccc;
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
        #profitSplitOptions {
            display: none;
            margin-left: 10px;
            padding: 10px;
            background: #f9f9f9;
            border-radius: 4px;
        }
        #profitSplitOptions div {
            padding: 5px;
            cursor: pointer;
        }
        #profitSplitOptions div:hover {
            background-color: #d0d0d0;
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
                <label>Profit Split Agreement:</label>
                <div id="profitSplitTap">Tap to Select Profit Split</div>
                <div id="profitSplitOptions">
                    <div data-split="50/50">50/50</div>
                    <div data-split="70/30">70/30</div>
                    <div data-split="80/20">80/20</div>
                </div>

                <div id="contributionDetails">
                    <h3>showTab - Contribution Breakdown</h3>
                    <p><strong>Account Price:</strong> <span id="accountPrice">TBD</span></p>
                    <p><strong>Profit Split:</strong> <span id="selectedProfitSplit">TBD</span></p>
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
            const profitSplitOptions = document.getElementById('profitSplitOptions');

            // Fixed account size and price (replace with API in production)
            const fixedAccountSize = '1000'; // $1,000 account
            const accountData = {
                '1000': 15 // $15 for $1,000, as per example
            };

            // Simulate API call to fetch price for account size
            function getPrice(size) {
                // TODO: Replace with actual API call, e.g.:
                // return fetch(`/api/propfirm/price?size=${size}`)
                //   .then(response => response.json())
                //   .then(data => data.price);
                return Promise.resolve(accountData[size] || 0);
            }

            // Selected profit split
            let currentProfitSplit = null;

            // Update contributions
            async function updateContributions() {
                const size = fixedAccountSize;
                const split = currentProfitSplit ? parseInt(currentProfitSplit.split('/')[0]) : 0;

                const price = await getPrice(size);

                accountPrice.textContent = price ? `$${price.toFixed(2)}` : 'TBD';
                selectedProfitSplit.textContent = currentProfitSplit || 'TBD';
                
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
                submitButton.disabled = !isEnabled;
                contributionDetails.style.display = isEnabled ? 'block' : 'none';
                profitSplitTap.style.pointerEvents = isEnabled ? 'auto' : 'none';
                profitSplitTap.style.backgroundColor = isEnabled ? '#e0e0e0' : '#cccccc';
                if (!isEnabled) {
                    profitSplitOptions.style.display = 'none';
                    accountPrice.textContent = 'TBD';
                    selectedProfitSplit.textContent = 'TBD';
                    requesterContribution.textContent = 'TBD';
                    partnerContribution.textContent = 'TBD';
                    result.textContent = '';
                } else {
                    updateContributions();
                }
            }

            // Toggle profit split options visibility
            profitSplitTap.addEventListener('click', () => {
                if (calculatorToggle.checked) {
                    profitSplitOptions.style.display = profitSplitOptions.style.display === 'block' ? 'none' : 'block';
                }
            });

            // Handle profit split selection
            profitSplitOptions.querySelectorAll('div').forEach(option => {
                option.addEventListener('click', () => {
                    currentProfitSplit = option.getAttribute('data-split');
                    profitSplitTap.textContent = `Profit Split Agreement: ${currentProfitSplit}`;
                    profitSplitOptions.style.display = 'none';
                    updateContributions();
                });
            });

            // Form submission
            form.addEventListener('submit', async (e) => {
                e.preventDefault();

                if (!calculatorToggle.checked) {
                    result.textContent = 'Co-Funding is turned off. Please turn it on to submit.';
                    result.className = 'error';
                    return;
                }

                if (!currentProfitSplit) {
                    result.textContent = 'Please select a profit split.';
                    result.className = 'error';
                    return;
                }

                const size = fixedAccountSize;
                const price = await getPrice(size);
                const requesterShare = (price * parseInt(currentProfitSplit.split('/')[0])) / 100;
                result.textContent = `Request submitted! Your contribution of $${requesterShare.toFixed(2)} is locked.`;
                result.className = '';
            });

            // Initial setup
            toggleCoFunding();
            updateContributions();
        });
    </script>
</body>
</html>

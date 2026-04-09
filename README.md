# ⚡ Opensea Drop NFT Minter (Enterprise Edition)

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Web3](https://img.shields.io/badge/Web3.py-v6.0%2B-orange?style=for-the-badge&logo=ethereum&logoColor=white)
![Status](https://img.shields.io/badge/Status-Production-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-lightgrey?style=for-the-badge)

**arinaakhipova** is a high-performance, asynchronous, and fully automated NFT Minting Bot designed for extreme speed "`War Mode`", massive scalability, and automated asset management. It features a sophisticated **Terminal User Interface (TUI)**, anti-honeypot security measures, and "`God Mode`" latency arbitrage strategies using pre-signed transactions.

---

## 📸 Interface Preview

The bot features a real-time, non-scrolling TUI Dashboard powered by the `rich` library.

```text
╭──────────────────────────────────────────────────────────────────────────╮
│       TARGET: 0x79f...d2ee | QTY: 1 | NETWORK: BASE                      │
╰──────────────────────────────────────────────────────────────────────────╯
                WORKER SQUADRON - Opensea drop bot by arinaakhipova
╭────┬──────────┬────────────────┬─────────────────────────────────────────╮
│ ID │   Time   │ Wallet Balance │ Status / Activity                       │
├────┼──────────┼────────────────┼─────────────────────────────────────────┤
│ 1  │ 13:45:10 │     0.0542 ETH │ [SUCCESS] Minted! TX: 0xabc...          │
│ 2  │ 13:45:11 │     0.0210 ETH │ [SUCCESS] Transferring to Cold Wallet...│
│ 3  │ 13:45:12 │     0.0000 ETH │ [WARNING] Insolvent. Waiting funder...  │
╰────┴──────────┴────────────────┴─────────────────────────────────────────╯
```

## 🚀 Key Features
### ⚔️ Sniper & Execution Engine
- ⚡ **God Mode (Pre-Signed Transactions):** Pre-calculates and signs raw transactions 5 seconds before the mint opens. Broadcasts instantly at T-0 (0ms CPU latency).

- 🕒 **Time Sniper:** Auto-sleeps and wakes up exactly when the mint starts (millisecond precision).

- 🎯 **Direct Mint Support:** Compatible with any contract function (e.g., `mint`, `publicMint`, `purchase`, `claim`) via Universal ABI.

- 🧠 **Local Nonce Caching:** Caches wallet nonces locally to eliminate RPC latency on sequential transactions.

### 🛡️ Security & Reliability
- 🕵️ **Anti-Honeypot (Contract Verifier):** Verifies if the contract source code is published on Etherscan/Basescan before allowing any transaction.

- 🔄 **RPC Rotator:** Automatically switches to backup nodes if the current node fails, timeouts, or hits rate limits.

- ⛽ **Shared Gas Oracle:** Reduces RPC calls by 95% using a shared global gas price cache for all workers.

- 🛡️ **Gas Guardian:** Pauses execution if network gas price exceeds your defined limit (Gwei).

### 💰 Asset Management
- ⛽ **Auto-Funder:** Master wallet automatically tops up worker wallets if the balance is insufficient before the war starts.

- 📦 **Auto-Consolidation:** Instantly transfers minted NFTs to your specified Cold Wallet.

- 🧹 **Dust Sweeper:** Automatically withdraws leftover ETH (gas change) back to the master wallet after execution.

- 📊 **The Accountant:** Logs every successful transaction, gas cost, and total spend to `history.csv` for PnL tracking.

### 📡 Telemetry & Reporting
- 🖥️ **Real-time TUI:** Beautiful, static dashboard monitoring worker status, balances, and system logs.

- 🔔 **Discord Notifications:** Reports successful mints and asset transfers via Webhook.

- 🕵️ **Diagnostics:** Secure endpoint using `RuntimeDiagnostics`.

## 📂 Project Structure
```Plaintext

arinaakhipova-minter/
├── .env                    # Configuration Secrets
├── main.py                 # Application Entry Point
├── private_key.txt         # Worker Private Keys
├── proxies.txt             # HTTP Proxies (Optional)
├── bot_activity.log        # detailed System Logs
├── history.csv             # Financial Records
├── requirements.txt        # Python Dependencies
└── src/
    ├── config/             # Settings & ABIs
    ├── engine/             # Core Logic (Executor)
    ├── features/           # Modules (Funder, Transfer, Accountant)
    ├── ui/                 # Display (TUI, Logger, Notifier)
    └── utils/              # Helpers (Verifier, Core Libs)
```

## 🛠️ Installation
**1. Prerequisites**
- Python 3.10 or higher.

- Git.

**2. Clone Repository**
```Bash
git clone https://github.com/arinaarkhipova/opensea-mint-war-bot.git
cd opensea-mint-war-bot
```
**3. Setup Virtual Environment**
**Windows (Git Bash):**

```Bash

python -m venv venv
source venv/Scripts/activate
```
**Linux/Mac:**

```Bash

python3 -m venv venv
source venv/bin/activate
```
**4. Install Dependencies**
```Bash

pip install -r requirements.txt
```
## ⚙️ Configuration
**1. Credentials**
- `private_key.txt`: Add your worker private keys here (one per line).

- `proxies.txt` (Optional): Add HTTP proxies `user:pass@ip:port` (one per line).

**2. Environment Variables (`.env`)**
Rename `.env.example` to `.env` and configure:

```Ini, TOML

# --- SYSTEM CONTRACTS ---
SEA_DROP_ADDRESS="0x00005EA00Ac477B1030CE78506496e8C2dE24bf5"
MULTIMINT_ADDRESS="0x0000419B4B6132e05DfBd89F65B165DFD6fA126F"

# --- NETWORK SELECTION ---
# Options: ETH, BASE, OP, ARB, POLY, AVAX, BSC, BERA, MONAD, ABSTRACT
NETWORK="ETH"

# --- TARGET MINTING ---
NFT_CONTRACT_ADDRESS="TheNFTContractAddressHere"
MINT_QUANTITY="1"

# --- TIME SNIPER ---
# Set ‘true’ to bypass the timer (mint immediately)
FORCE_START=false

# --- MINTING MODE ---
# Mode: ‘PROXY’ (Default, via MultiMint) or ‘DIRECT’ (Directly to the target contract)
MINT_MODE="DIRECT"

# Minting Function Name (Only for DIRECT mode)
# Check on Etherscan (Write Contract). Common examples: ‘mint’, ‘publicMint’, “purchase”, ‘claim’
MINT_FUNC_NAME="mint"

# --- PROXY SETTINGS ---
# Set ‘true’ to use proxies from proxies.txt
# Set ‘false’ to run the bot directly (without proxy)
USE_PROXIES=false

# --- PERFORMANCE ---
MAX_WORKERS="5"
RETRY_DELAY_MIN="1.5"
RETRY_DELAY_MAX="3.0"
# Leave blank for automatic. Enter a number (e.g. 5) to force a specific Gwei.
GAS_PRICE_GWEI=""

# --- GAS GUARDIAN ---
# Maximum Gwei limit. If network gas > this, bot PAUSES.
MAX_GAS_LIMIT="50"

# --- GOD MODE (PRE-SIGNED TX) ---
# Set ‘true’ to prepare transactions before minting time arrives
PRE_SIGN_ENABLED=false
# Gas Price Buffer (Multiplier) for Pre-Sign.
# 2.0 means we set the gas to 2x the current price so that the TX doesn't get stuck during the war.
PRE_SIGN_GAS_MULTIPLIER="2.0"
# Hardcoded Gas Limit (because estimates often fail before minting opens)
# Standard NFT mint: 150000 - 300000
PRE_SIGN_GAS_LIMIT="300,000"

# --- AUTO FUNDER (GAS DISPENSER) ---
# Set to ‘true’ to enable
AUTO_FUND_ENABLED=false
# Main Wallet Private Key (Master) that will send ETH to workers
MASTER_PRIVATE_KEY="0xYourMasterPrivateKeyHere"
# What is the minimum balance a worker must have? (e.g. 0.005 ETH)
# If it is less than this, the Master will transfer.
MIN_WORKER_BALANCE="0.005"
# How much will be transferred if the balance is insufficient? (Top-up Amount)
FUNDING_AMOUNT="0.01"

# --- WALLET CLEANER ---
# Set ‘true’ to withdraw the remaining ETH to the Recipient Address after minting is complete
AUTO_SWEEP_ETH=false
# Minimum balance that can be withdrawn (to avoid losing money on fees). Example: 0.005 ETH
MIN_ETH_TO_SWEEP="0.005"

# --- AUTO TRANSFER / CONSOLIDATION ---
# Set ‘true’ to enable the feature to send NFTs to Cold Wallet
AUTO_TRANSFER_ENABLED=false
RECIPIENT_ADDRESS="0xYourMainWalletAddressHere"

# --- NOTIFICATION SYSTEM ---
DISCORD_ENABLED=false
DISCORD_WEBHOOK_URL="https://discord.com/api/webhooks/xxxx/xxxx"

# --- THE ACCOUNTANT (BOOKKEEPING) ---
# Set ‘true’ to record transaction history to the history.csv file.
ACCOUNTANT_ENABLED=false

# --- ANTI-HONEYPOT / VERIFIER ---
# Set to ‘true’ to check whether the contract source code has been verified before minting.
VERIFY_CONTRACT_ENABLED=false
# Enter API Key Explorer (Etherscan/Basescan/Arbiscan according to network)
# Register for free at: https://basescan.org/myapikey (Example for BASE)
EXPLORER_API_KEY="YourExplorerApiKeyHere"
```
**3. How to get the nft contract**
 - Go to website https://opensea.io/drops
   
 - Open the `NFT minting pages`
   
 - then copy contract (check the image below)
<img width="360" height="100" alt="image" src="https://github.com/user-attachments/assets/3643ab68-113a-48b2-ad07-8431004fa3e3" />

## 🏃 Usage
Run the bot using Python:

```Bash

python main.py
```
- **Exit:** Press `CTRL+C` safely to stop the bot.

- **Monitoring:** Watch the TUI on your screen.

- **Logs:** Check `bot_activity.log` for detailed technical logs if errors occur.

- **Profit/Loss:** Open `history.csv` in Excel/Numbers to track expenses.

## 🔮 Roadmap (V2 Premium Features)
The following features are currently under development:

- [ ] 🐋 **Shadow Copy-Minting:** Detects "Whale/Influencer" transactions in the mempool and automatically copies their mints instantly.

- [ ] ⚡ **Mempool Sniper (Block 0):** Detects Developer's "Enable Mint" transaction and back-runs it within the same block.

- [ ] 📱 **Telegram Command Center:** Full remote control (Stop/Start/Withdraw) via a 2-way Telegram Bot.

- [ ] 🛒 **Instant Flipper:** Automatically lists minted NFTs on OpenSea/Blur based on floor price logic.

- [ ] 📜 **Merkle Proof Handler:** Automated support for Whitelist/Allowlist minting phases with proof injection.

## ⚠️ Disclaimer

**STRICT WARNING:**
This software (`arinaakhipova`) is created solely for **educational and experimental purposes**. Using this bot for activities on the mainnet (such as Ethereum/Base) involves real financial risks.

**By using this software, you agree that:**  
> 1. The developer is **not liable** for financial losses (Gas fees, Rug pulls, Mistaken purchases).  
> 2. The developer is **not liable** if your wallet is blocked or marked as a Sybil.
> 3. You use this bot entirely at your own risk (DWYOR - Do With Your Own Risk).

**arinaakhipova Team** © 2025
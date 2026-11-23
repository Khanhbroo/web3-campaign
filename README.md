# 🌐 Web3 Campaign — Decentralized Crowdfunding Platform & dApp

<div align="center">

**A production-ready decentralized crowdfunding application engineered with React 19, Ethers.js v6, Reown AppKit (WalletConnect), and Solidity on Ethereum Sepolia.**

Trustless campaign origination, non-custodial ETH funding, real-time blockchain event indexing, and gas-efficient EVM smart contract execution.

[![Live Demo](https://img.shields.io/badge/GitHub_Pages-Live_dApp-10b981?style=for-the-badge&logo=safari&logoColor=white)](https://khanhbroo.github.io/web3-campaign/)
[![GitHub Repo](https://img.shields.io/badge/GitHub-Khanhbroo%2Fweb3--campaign-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Khanhbroo/web3-campaign)
[![React 19](https://img.shields.io/badge/React-19.0-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev)
[![Ethers.js v6](https://img.shields.io/badge/Ethers.js-v6.13-2535A0?style=for-the-badge&logo=ethereum&logoColor=white)](https://docs.ethers.org/v6/)
[![Reown AppKit](https://img.shields.io/badge/Reown_AppKit-WalletConnect-3396FF?style=for-the-badge&logo=walletconnect&logoColor=white)](https://reown.com)
[![Solidity](https://img.shields.io/badge/Solidity-0.8.x-363636?style=for-the-badge&logo=solidity&logoColor=white)](https://soliditylang.org)
[![Sepolia Testnet](https://img.shields.io/badge/Ethereum-Sepolia_Testnet-627EEA?style=for-the-badge&logo=ethereum&logoColor=white)](https://sepolia.etherscan.io)
[![Tailwind CSS v4](https://img.shields.io/badge/Tailwind_CSS-v4.0-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com)

</div>

---

## 🚀 Live dApp & Smart Contract Deployment

- 🌐 **Live Web3 Application**: [https://khanhbroo.github.io/web3-campaign/](https://khanhbroo.github.io/web3-campaign/)
- 📜 **Sepolia Smart Contract**: [`0x954eAE984E4091b8aA6f9060C9e8A35fb9955aC1`](https://sepolia.etherscan.io/address/0x954eAE984E4091b8aA6f9060C9e8A35fb9955aC1)
- 📦 **GitHub Repository**: [https://github.com/Khanhbroo/web3-campaign](https://github.com/Khanhbroo/web3-campaign)

---

## 🌟 Executive Overview

**Web3 Campaign** eliminates the centralized intermediaries, fee extraction, and censorship risks of traditional crowdfunding platforms (e.g., Kickstarter, GoFundMe) by deploying trustless, immutable smart contracts on Ethereum.

Built with **React 19**, **Ethers.js v6**, and the modern **Reown AppKit** (formerly Web3Modal), the dApp offers a frictionless Web3 onboarding experience: users connect any EVM wallet, create campaigns with milestone goals, donate ETH directly through cryptographically verified transactions, and track on-chain campaign milestones in real time.

---

## ⚡ Core Engineering & Blockchain Architecture

### 1. 🛡️ Smart Contract Specification (Sepolia EVM)
The core contract (`CrowdFunding.sol`) deployed at `0x954eAE984E4091b8aA6f9060C9e8A35fb9955aC1` enforces:
- **`createCampaign`**: Takes title, description, target (in wei), deadline (UNIX timestamp), and image URI; pushes to storage array and emits unique `campaignId`.
- **`fundToCampaign`**: Payable function receiving ETH, verifying campaign status, incrementing `amountCollected`, registering funder addresses, and emitting `CampaignFunded(campaignId, funder, amount)`.
- **`getCampaigns`**: Gas-optimized read query batch-returning all campaign structures (`owner`, `title`, `description`, `target`, `deadline`, `image`, `amountCollected`, `funders`, `funded`).
- **`getFunders`**: Retrieves historical donor addresses alongside corresponding contribution amounts for complete public auditability.

### 2. 🔌 Dual-Provider Provider Pattern (`BrowserProvider` + `AlchemyProvider`)
To ensure optimal performance and frictionless user experience:
- **Active Wallet Mode**: When a user connects their wallet via Reown AppKit, the app instantiates an Ethers.js `BrowserProvider(walletProvider)` with an active `Signer` to execute payable transactions.
- **Passive Read-Only Mode**: When no wallet is connected, the app seamlessly falls back to an `AlchemyProvider('sepolia', API_KEY)` instance. Visitors can browse active campaigns, inspect funding progress, and view donor rosters without being forced to connect a wallet first.

### 3. 💼 Modern Multi-Wallet Handshake (`Reown AppKit`)
- Powered by `@reown/appkit` and `@reown/appkit-adapter-ethers`.
- Universal support across 300+ crypto wallets: MetaMask, Coinbase Wallet, Rainbow, Trust Wallet, and WalletConnect QR scanning for mobile devices.
- Seamless network switching and automatic handling of `accountsChanged` and `chainChanged` events.

### 4. 📊 Real-Time Financial Formatting & Progress Calculations
- Precision unit conversion between human-readable ETH and EVM integer representations via `parseEther()` and `formatEther()`.
- Dynamic percentage computation with remaining days countdown logic based on smart contract UNIX timestamps.
- Donor leaderboard dynamically mapping addresses to contribution sizes.

---

## 🛠️ Technology Stack

| Layer | Technologies | Role in System |
| :--- | :--- | :--- |
| **Frontend Framework** | React 19.0, Vite 6.1 | Concurrent React rendering and instant HMR dev server |
| **Blockchain Client** | Ethers.js v6.13, Alchemy RPC | EVM smart contract bindings, ABI decoding, and transaction handling |
| **Wallet Connector** | Reown AppKit v1.6 (WalletConnect) | Multi-wallet discovery, QR modals, and session management |
| **Smart Contract** | Solidity 0.8.x, Ethereum Sepolia | Autonomous on-chain escrow, campaign storage, and fund disbursement |
| **Styling & Icons** | Tailwind CSS v4, Lucide React | Modern dark-mode UI with high-density data cards |
| **Routing & Deployment**| React Router DOM v7.2, GitHub Pages | Client-side routing and automated CI/CD static hosting |

---

## 🏗️ Codebase Hierarchy

```text
web3-campaign/
├── public/                # Static public assets
├── src/
│   ├── assets/            # SVG icons, logos, and UI graphics
│   ├── components/        # Reusable UI components
│   │   ├── Button.jsx             # Interactive Web3 button with loading states
│   │   ├── CountBox.jsx           # Milestone statistic counter card
│   │   ├── DisplayCampaign.jsx    # Responsive grid feed rendering active campaigns
│   │   ├── FormField.jsx          # Type-safe input wrappers with dark-theme styling
│   │   ├── FundCard.jsx           # Individual campaign metric card with progress bar
│   │   ├── Icon.jsx               # Navigation & social icon renderer
│   │   ├── Loader.jsx             # Transaction pending spinner overlay
│   │   ├── Navbar.jsx             # Top bar with Reown wallet connect button
│   │   ├── Sidebar.jsx            # Desktop icon navigation rail
│   │   └── index.js               # Central barrel exports
│   ├── constants/         # Static navigation links and configuration
│   ├── context/
│   │   └── index.jsx      # Global Web3 context provider (StateContextProvider)
│   ├── contracts/
│   │   └── contractData.js # Sepolia contract address & complete ABI definition
│   ├── pages/
│   │   ├── Home.jsx               # Feed of all active crowdfunding campaigns
│   │   ├── CreateCampaign.jsx     # On-chain campaign deployment form
│   │   ├── CampaignDetails.jsx    # Donor details, progress bar, and ETH funding form
│   │   ├── Profile.jsx            # User-centric view of created & funded campaigns
│   │   └── index.js               # Barrel export for pages
│   ├── utils/             # ETH calculation and date formatting utilities
│   ├── App.jsx            # Master layout containing Navbar, Sidebar, and App Router
│   ├── index.css          # Tailwind CSS v4 style directives
│   └── main.jsx           # Entry point wrapped with BrowserRouter & StateContext
├── eslint.config.js       # ESLint 9 configuration
├── index.html             # HTML entry shell
├── package.json           # Dependencies and gh-pages deployment scripts
└── vite.config.js         # Vite 6 configuration
```

---

## ⚙️ Environment Configuration

Create a `.env` file in the project root with the following keys:

```env
# Reown (WalletConnect) Cloud Project ID
VITE_WALLET_CONNECT_ID=your_reown_project_id

# Alchemy Sepolia RPC URL
VITE_ETH_SEPOLIA_RPC_URL=https://eth-sepolia.g.alchemy.com/v2/your_alchemy_key

# Alchemy Sepolia API Key for fallback read provider
VITE_ALCHEMY_SEPOLIA_KEY=your_alchemy_sepolia_api_key
```

> **Smart Contract Suite:** The underlying EVM smart contracts, Chainlink price oracles, and Forge deployment scripts are maintained in the [web3-campaign-foundry](https://github.com/Khanhbroo/web3-campaign-foundry) repository.

> **Where to get keys:**
> - **Reown Project ID**: Sign up free at [Reown Cloud](https://cloud.reown.com).
> - **Alchemy Key**: Generate an Ethereum Sepolia app at [Alchemy Dashboard](https://dashboard.alchemy.com).

---

## 🚀 Quickstart & Local Execution

### 1. Clone & Install
```bash
# Clone the repository
git clone https://github.com/Khanhbroo/web3-campaign.git

# Enter project directory
cd web3-campaign

# Install dependencies
npm install
```

### 2. Run Local Development Server
```bash
npm run dev
```
Open `http://localhost:5173` in your browser. Connect MetaMask to the **Sepolia Testnet** to test campaign creation and donations.

### 3. Deploy to GitHub Pages
```bash
npm run deploy
```

---

## 👨‍💻 Author & Engineering Profile

**Nguyen Quoc Khanh (KhanhBro)**  
*Senior Full-Stack Software Engineer & Creative UI Architect*  
- **GitHub**: [@Khanhbroo](https://github.com/Khanhbroo)  
- **Live dApp**: [https://khanhbroo.github.io/web3-campaign/](https://khanhbroo.github.io/web3-campaign/)  
- **Portfolio**: [Interactive macOS Web OS](https://macos-portfolio-khanhbroo.vercel.app)  
- **Email**: [khanhmathias532211@gmail.com](mailto:khanhmathias532211@gmail.com)  

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

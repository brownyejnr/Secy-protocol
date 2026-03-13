[README.md](https://github.com/user-attachments/files/25961189/README.md)
# ⚡ STREAK PROTOCOL
### All-in-One Bitcoin DeFi Super-App on OP_NET
**OP_NET Vibecoding Challenge — Week 3: The Breakthrough**

---

```
███████╗████████╗██████╗ ███████╗ █████╗ ██╗  ██╗
██╔════╝╚══██╔══╝██╔══██╗██╔════╝██╔══██╗██║ ██╔╝
███████╗   ██║   ██████╔╝█████╗  ███████║█████╔╝ 
╚════██║   ██║   ██╔══██╗██╔══╝  ██╔══██║██╔═██╗ 
███████║   ██║   ██║  ██║███████╗██║  ██║██║  ██╗
╚══════╝   ╚═╝   ╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝
PROTOCOL — BITCOIN L1 DEFI TERMINAL
```

## Overview

Streak Protocol is a full-stack DeFi super-app demonstrating that Bitcoin Layer 1 can host advanced DeFi ecosystems via OP_NET. It ships three production-grade smart contracts and a complete Crimson Matrix-themed frontend.

| Module | Contract | Description |
|--------|----------|-------------|
| NFT Marketplace | `StreakMarket` | Trustless OP_721 exchange with floor price tracking |
| Lending Platform | `StreakLend` | OP_20 lending pool with APY math & LTV enforcement |
| DAO Hub | `StreakDAO` | On-chain governance, treasury management, proposals |

---

## Architecture

```
streak-protocol/
├── contracts/
│   ├── streak-market/     # OP_721 NFT exchange (AssemblyScript)
│   │   └── src/
│   │       ├── StreakMarket.ts
│   │       └── index.ts
│   ├── streak-lend/       # OP_20 lending pool (AssemblyScript)
│   │   └── src/
│   │       ├── StreakLend.ts
│   │       └── index.ts
│   └── streak-dao/        # Governance hub (AssemblyScript)
│       └── src/
│           ├── StreakDAO.ts
│           └── index.ts
├── frontend/
│   └── index.html         # Production-ready single-file DApp
├── tests/
│   └── streak-protocol.test.ts
├── AUDIT_REPORT.md
├── vercel.json
└── package.json
```

---

## Smart Contract Highlights

### StreakMarket
- Trustless peer-to-peer NFT exchange for OP_721 artifacts
- Live floor price tracking (updates on every listing)
- Cumulative volume tracking
- Reentrancy guard + pause mechanism
- `listItem` / `buyItem` / `cancelListing` / `getListing` / `floorPrice`

### StreakLend
- Single-asset supply/borrow pool
- Linear interest accrual per block (base APY × utilisation)
- 75% LTV cap enforced on-chain
- Liquidation for unhealthy positions
- NFT collateral architecture prepared (activates in v1.1)
- Flash loan architecture documented

### StreakDAO
- Multi-DAO registry with independent treasuries
- Token-weighted voting (1 token = 1 vote)
- Configurable quorum (basis points) + voting period (blocks)
- Double-vote prevention via composite storage key
- Proposal lifecycle: PENDING → ACTIVE → SUCCEEDED/DEFEATED → EXECUTED

---

## Security

All contracts implement:
- **Checks-Effects-Interactions** pattern throughout
- **Reentrancy guard** (`_reentrancyLock`) on all write paths
- **SafeMath** for every arithmetic operation
- **Admin-only** admin functions via `onlyDeployer(Blockchain.tx.sender)`
- **Pause switch** for emergency halt
- **No floating-point** — all rates use basis-point integer math
- **`@final`** decorator prevents unsafe contract extension

See `AUDIT_REPORT.md` for the full OpnetAudit findings.

---

## Quick Start

### Prerequisites
```bash
node >= 18
npm >= 9
```

### Install
```bash
npm install
```

### Build Contracts
```bash
# Individual contracts
cd contracts/streak-market && npm install && npm run build
cd contracts/streak-lend   && npm install && npm run build
cd contracts/streak-dao    && npm install && npm run build
```

### Run Tests
```bash
npx opnet-unit-test ./tests/streak-protocol.test.ts
```

### Run Frontend Locally
```bash
# Open frontend/index.html directly in browser, or:
cd frontend && npx serve .
```

---

## Deployment

### Deploy Frontend to Vercel

```bash
# One-command Vercel deployment (from project root):
npx vercel --prod --yes
```

The `vercel.json` is pre-configured for instant deployment. Vercel will output a live URL.

### Deploy Contracts to OP_NET Testnet

```bash
# Compile to WASM
cd contracts/streak-market && npm run build

# Deploy using opnet CLI
npx opnet deploy \
  --network testnet \
  --wasm contracts/streak-market/build/release.wasm \
  --wallet YOUR_WALLET_KEY

# Repeat for streak-lend and streak-dao
```

> Use OP_NET testnet (Signet fork at `https://testnet.opnet.org`) — NOT Bitcoin Testnet4.

---

## Frontend Features

- **Crimson Matrix Theme** — Pure pitch-black background with deep maroon glass panels
- **Matrix Rain Effect** — HTML5 Canvas animation in crimson shades at 17% opacity
- **Glassmorphic Navigation** — Blur backdrop, maroon glow borders, smooth routing
- **OP_WALLET Integration** — Connect button with live address/balance state
- **NFT Grid** — Responsive 4-col → 2-col → 1-col with filter/sort/search
- **Lending Dashboard** — Dual-pane supply/borrow with live LTV health bar
- **DAO Hub** — Voting progress bars, treasury overview, proposal workflow
- **Tooltips** — Hover-triggered definitions for APY, Floor Price, LTV, Flash Loans
- **Toast Notifications** — Slide-in transactions: Pending → Success/Error
- **Mobile Responsive** — Hamburger menu, adaptive grids, fluid typography
- **FAQ Footer** — Six common DeFi questions answered inline

---

## Environment Variables

```env
NEXT_PUBLIC_OPNET_NETWORK=mainnet
NEXT_PUBLIC_OPNET_RPC=https://api.opnet.org
```

---

## License

MIT — Built for the OP_NET Vibecoding Challenge Week 3.

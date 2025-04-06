# Nexus Champions Protocol - Smart Contract Documentation

**A Bitcoin-Layer 2 Gaming Protocol on Stacks**  
_Version 1.0.0 | Compliant with Clarity v2.x_

---

## Table of Contents

1. [Protocol Overview](#protocol-overview)
2. [Core Features](#core-features)
3. [Technical Architecture](#technical-architecture)
4. [Error Handling](#error-handling)
5. [Installation & Deployment](#installation--deployment)
6. [Usage Examples](#usage-examples)
7. [Security Considerations](#security-considerations)
8. [Contributing](#contributing)

---

## Protocol Overview

Nexus Champions is a decentralized gaming protocol enabling:

- NFT-based in-game assets with upgradable metadata
- Avatar progression systems with Bitcoin-denominated rewards
- Multi-world environments with entry requirements
- Provably fair competitive leaderboards
- STX/BTC hybrid economic model

Built on Stacks Layer 2 for Bitcoin finality and Clarity smart contracts for formal verification.

---

## Core Features

### 1. NFT Asset Management

- Minting of game assets with 10+ metadata attributes
- Cross-world compatibility through `world-access` lists
- Experience-based asset leveling system

### 2. Avatar System

- Customizable player profiles with:
  - 100-level progression
  - Achievement tracking
  - Equipment loadouts
- World access control lists

### 3. Virtual Worlds

- Permissioned environments with:
  - Entry fee requirements
  - Active player tracking
  - Reward pool management

### 4. Competitive Leaderboard

- Score-based ranking system
- Bitcoin reward distribution channels
- Game statistics tracking:
  - Total rewards earned
  - Games played
  - Achievement milestones

### 5. Bitcoin Integration

- sBTC-wrapped reward pools
- Lightning Network compatible microtransactions
- Bitcoin block height-triggered events

---

## Technical Architecture

### Key Components

| Component      | Type | Description                         |
| -------------- | ---- | ----------------------------------- |
| `nexus-asset`  | NFT  | In-game items with upgradable stats |
| `nexus-avatar` | NFT  | Player identity and progression     |
| `game-worlds`  | Map  | Virtual environment configurations  |
| `leaderboard`  | Map  | Competitive player rankings         |

### Configuration Variables

```clarity
(define-data-var protocol-fee uint u10)
(define-data-var max-leaderboard-entries uint u50)
(define-data-var total-prize-pool uint u0)
```

### Validation System

- 15+ validation functions including:
  - `is-valid-name` (50 char limit)
  - `is-valid-rarity` (5-tier system)
  - `is-valid-power-level` (1-1000 range)
  - `is-valid-world-access` (cross-chain checks)

---

## Error Handling

### Error Code Matrix

| Error Constant           | Code | Description                 |
| ------------------------ | ---- | --------------------------- |
| `ERR-NOT-AUTHORIZED`     | u1   | Unauthorized access attempt |
| `ERR-INVALID-GAME-ASSET` | u2   | Nonexistent asset reference |
| `ERR-INSUFFICIENT-FUNDS` | u3   | Balance check failure       |
| ...                      | ...  | ...                         |
| `ERR-MAX-LEVEL-REACHED`  | u22  | Level cap enforcement       |

---

## Installation & Deployment

### Requirements

- Clarinet v2.0+
- Stacks.js
- Bitcoin testnet node

### Deployment Steps

1. Clone repository:
   ```bash
   git clone https://github.com/nexus-champions/core-contracts.git
   ```
2. Install dependencies:
   ```bash
   npm install
   ```
3. Configure network settings in `settings/Development.toml`
4. Deploy contract:
   ```bash
   clarinet deploy --network testnet
   ```

---

## Usage Examples

### 1. Minting Game Asset

```clarity
(contract-call? 'nexus-champions mint-nexus-asset
  "Dragon Sword"
  "Legendary weapon"
  "legendary"
  u950
  u1
  (list "fire" "sharpness")
```

### 2. Avatar Creation

```clarity
(contract-call? 'nexus-champions create-avatar
  "WarriorClass"
  (list u1 u2 u3))
```

### 3. Leaderboard Update

```clarity
(contract-call? 'nexus-champions update-player-score
  'ST1PQHQKV0RJXZFY1DGX8MNSNYVE3VGZJSRTPGZGM
  u1500)
```

### 4. Reward Distribution

```clarity
(contract-call? 'nexus-champions distribute-bitcoin-rewards)
```

---

## Security Considerations

### Formal Verification

- All functions include:
  - Pre-condition checks
  - Post-condition validation
  - Overflow/underflow protection

### Audit Recommendations

1. Use multisig for admin functions
2. Implement reentrancy guards
3. Regular snapshot backups

---

## Contributing

1. Fork repository
2. Create feature branch (`feat/feature-name`)
3. Submit PR with:
   - Test coverage
   - Documentation updates
   - Clarity-lint results

# DonCoin Platform

DonCoin is a decentralized crowdfunding platform designed for fair, transparent, and community-driven funding of public goods and open-source projects. The platform combines a **web frontend**, a **Django backend**, a **PostgreSQL database**, and **smart contracts on Ethereum** to handle donations, quadratic funding, and governance.

---

## Table of Contents

- [Features](#features)
- [Architecture Overview](#architecture-overview)
- [Backend](#backend)
- [Frontend](#frontend)
- [Database](#database)
- [Smart Contracts](#smart-contracts)
- [Installation & Setup](#installation--setup)
- [Seeding Data](#seeding-data)
- [Usage](#usage)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- **Wallet Management**: Users have wallets with balances, statuses, and activity logs.
- **Donor Profiles**: Donors can contribute to proposals and have reputation scores.
- **Sybil Protection**: Wallets have Sybil scores verified by trusted parties.
- **Quadratic Funding Rounds**: Proposals compete for matching funds in rounds.
- **Proposals & Donations**: Donors can fund proposals; total donations tracked.
- **Matching & Payouts**: Matches are calculated, and payouts are distributed automatically.
- **Governance**: Users can hold governance tokens with voting power and roles.
- **Smart Contract Events**: All key actions are logged on-chain for transparency.

---

## Architecture Overview

```text
+----------------+        +-----------------+       +-------------------+
|                |        |                 |       |                   |
|   Frontend     +------->+     Backend     +------>+      Database      |
| (Next.js/React)|        |  (Django REST)  |       |  (PostgreSQL)     |
|                |        |                 |       |                   |
+-------+--------+        +--------+--------+       +-------------------+
        |                         |
        |                         |
        v                         v
   Smart Contract (Ethereum / EVM) logs transactions, donations, and matches
Backend
Built with Django and Django REST Framework.

Handles:

CRUD operations for wallets, donors, proposals, donations, rounds, and pools.

Sybil score verification.

Quadratic funding calculations.

Payout processing.

Smart contract event logging.

Key packages:

django

djangorestframework

psycopg2-binary (PostgreSQL)

Faker (for synthetic data)

uuid for unique identifiers.

Frontend
Built with Next.js (React-based framework).

Responsibilities:

Display proposals, rounds, and matching pools.

Allow donors to connect wallets and make donations.

Show governance and voting dashboard.

Interact with backend APIs for data.

Optionally, interact directly with smart contracts via Web3 or ethers.js.

Database
PostgreSQL is used as the main relational database.

Models include:

Wallet, Donor, SybilScore

MatchingPool, Round, Proposal, Donation, Match, QFResult, Payout, ContractEvent, GovernanceToken

Relationships:

One-to-many: Wallet → Donors, Wallet → SybilScores

Many-to-one: Proposals → Round, Donations → Proposal, Matches → Proposal

Unique constraints enforced for tx_hash, usernames, and wallet roles.

Smart Contracts
Written in Solidity for Ethereum / EVM-compatible networks.

Responsibilities:

Record donations and matches.

Log contract events for transparency.

Handle payouts if fully on-chain.

Can be interacted via frontend with Web3.js or ethers.js.

Installation & Setup
Backend
bash
Kodu kopyala
git clone <repo_url>
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
Frontend
bash
Kodu kopyala
cd frontend
npm install
npm run dev
Environment Variables
Create .env files for backend and frontend:

env
Kodu kopyala
# Backend
DATABASE_URL=postgres://user:password@localhost:5432/doncoin
SECRET_KEY=your_django_secret_key

# Frontend
NEXT_PUBLIC_API_URL=http://localhost:8000/api
Seeding Data
Use the seed_data.py script in the backend to populate fake data:

bash
Kodu kopyala
python scripts/seed_data.py
This will generate:

Wallets, donors, and Sybil scores

Matching pools and rounds

Proposals and donations

Matches, QF results, payouts

Governance tokens and contract events

Usage
Start the backend:

bash
Kodu kopyala
python manage.py runserver
Start the frontend:

bash
Kodu kopyala
npm run dev
Access the application at http://localhost:3000.

Use the Django admin at http://localhost:8000/admin for direct management.

Contributing
Fork the repository.

Create a feature branch: git checkout -b feature/your-feature

Commit changes: git commit -am 'Add your feature'

Push to branch: git push origin feature/your-feature

Open a Pull Request.


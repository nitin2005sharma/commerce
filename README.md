# Full-Stack Ecommerce Platform

This project is a modern ecommerce platform built with a `Next.js` frontend and an `Express + Prisma` backend. It supports a customer storefront, admin dashboard, Stripe checkout, real-time chat, shared-cart collaboration, guided goal-based shopping, checkout recovery, order tracking, and post-purchase support workflows.

## Documentation

The complete structured documentation is in [`docs/README.md`](./docs/README.md).

- [`docs/FEATURES.md`](./docs/FEATURES.md): feature-by-feature application guide
- [`docs/ARCHITECTURE.md`](./docs/ARCHITECTURE.md): frontend, backend, data, API, and integration architecture
- [`docs/FILE_STRUCTURE.md`](./docs/FILE_STRUCTURE.md): route, module, and important file map
- [`docs/API_REFERENCE.md`](./docs/API_REFERENCE.md): REST, GraphQL, RTK Query, and Socket.IO reference
- [`docs/DATA_MODEL.md`](./docs/DATA_MODEL.md): Prisma models, enums, and relationships
- [`docs/RUNBOOK.md`](./docs/RUNBOOK.md): setup, commands, verification, and troubleshooting

## Overview

- `src/client` contains the Next.js frontend
- `src/server` contains the Express, Prisma, and Socket.IO backend
- `PostgreSQL` is the primary database
- `Redis` supports runtime infrastructure such as sessions and cache-style flows

## Core Features

- Product browsing, filtering, variants, reviews, and category management
- Customer authentication with email/password and social login support
- Persistent carts, checkout attempts, checkout recovery, and Stripe payments
- Orders, payments, shipments, transactions, and public order tracking
- Live support chat with Socket.IO and WebRTC signaling
- Shared-cart collaboration with votes, notes, and real-time updates
- Goal-based bundle building for guided shopping
- Post-purchase order companion and goal success tracking
- Admin dashboards for products, categories, attributes, inventory, users, logs, reports, chats, analytics, and transactions

## Architecture

```mermaid
flowchart LR
    U["Customer"] --> FE["Next.js Frontend"]
    A["Admin / Support"] --> FE

    FE --> API["Express API + GraphQL + Socket.IO"]

    API --> AUTH["Auth Module"]
    API --> SHOP["Catalog / Cart / Checkout / Orders"]
    API --> LIVE["Chat / Shared Cart / Order Updates"]
    API --> OPS["Analytics / Reports / Logs"]

    AUTH --> DB["PostgreSQL via Prisma"]
    SHOP --> DB
    LIVE --> DB
    OPS --> DB

    API --> REDIS["Redis"]
    API --> STRIPE["Stripe"]
    API --> CLOUD["Cloudinary"]

    API -. realtime .-> FE
```

## Tech Stack

### Frontend

- `Next.js 15`
- `React 19`
- `TypeScript`
- `Tailwind CSS 4`
- `Redux Toolkit` and `RTK Query`
- `Apollo Client`
- `Framer Motion`
- `ApexCharts`
- `Socket.IO Client`
- `Stripe.js`

### Backend

- `Node.js`
- `Express`
- `TypeScript`
- `Prisma ORM`
- `Apollo Server`
- `Socket.IO`
- `Passport`
- `JWT`
- `Winston`
- `Swagger`
- `Nodemailer`

### Data and Services

- `PostgreSQL`
- `Redis`
- `Stripe`
- `Cloudinary`
- `Google OAuth`
- `Facebook OAuth`
- `Twitter OAuth`

## Project Structure

```text
ecommerce/
|-- src/
|   |-- client/
|   |   |-- app/
|   |   |-- public/
|   |   `-- package.json
|   |-- server/
|   |   |-- prisma/
|   |   |-- seeds/
|   |   |-- src/
|   |   |   |-- infra/
|   |   |   |-- modules/
|   |   |   `-- shared/
|   |   `-- package.json
|   |-- .env.example
|   |-- client/.env.example
|   `-- server/.env.example
|-- assets/
|-- collections/
`-- README.md
```

## Main Backend Modules

- `auth`
- `user`
- `product`
- `category`
- `attribute`
- `variant`
- `cart`
- `checkout`
- `order`
- `payment`
- `shipment`
- `transaction`
- `review`
- `chat`
- `goal`
- `shared-cart`
- `analytics`
- `reports`
- `logs`
- `webhook`
- `address`

## Local Setup

### Prerequisites

- `Node.js` 20+ or newer
- `npm`
- `PostgreSQL`
- `Redis`

### 1. Install dependencies

```powershell
npm install
Set-Location .\src\server
npm install
Set-Location ..\client
npm install
Set-Location ..\..
```

### 2. Configure environment files

Copy these example files and fill in your real values:

- [src/.env.example](./src/.env.example)
- [src/client/.env.example](./src/client/.env.example)
- [src/server/.env.example](./src/server/.env.example)

Typical local values:

```env
# src/server/.env
DATABASE_URL=postgresql://postgres:password@localhost:5432/ss_commerce
NODE_ENV=development
PORT=5000
REDIS_URL=redis://localhost:6379
CLIENT_URL_DEV=http://localhost:3000
ALLOWED_ORIGINS=http://localhost:3000
ACCESS_TOKEN_SECRET=change-me
REFRESH_TOKEN_SECRET=change-me
SESSION_SECRET=change-me
COOKIE_SECRET=change-me
```

```env
# src/client/.env.local
NEXT_PUBLIC_API_URL=http://localhost:5000/api/v1
NEXT_PUBLIC_API_URL_DEV=http://localhost:5000/api/v1
NEXT_PUBLIC_API_URL_PROD=http://localhost:5000/api/v1
NODE_ENV=development
```

### 3. Run Prisma migrations

```powershell
Set-Location .\src\server
npx prisma migrate dev
npx prisma generate
```

### 4. Seed the database

```powershell
npm run seed
```

### 5. Start the app

Backend:

```powershell
Set-Location .\src\server
npm run dev
```

Frontend:

```powershell
Set-Location .\src\client
npm run dev
```

## Local URLs

- Frontend: `http://localhost:3000`
- Backend API: `http://localhost:5000/api/v1`
- GraphQL: `http://localhost:5000/api/v1/graphql`
- Swagger docs: `http://localhost:5000/api-docs`
- Health check: `http://localhost:5000/health`

## Key User Flows

### Customer

- Browse products and categories
- Add items to cart
- Complete checkout
- View order details and tracking
- Use support chat when needed

### Shared Cart

- Create a shared cart from the normal cart
- Send the share link/code
- Collaborators join, vote, add notes, and update quantities live

### Goal-Based Shopping

- Open a goal template
- Choose a budget
- Receive a recommended bundle from in-stock products

### Admin

- Manage products, categories, attributes, and inventory
- Track transactions and update shipping progress
- Respond to support chats
- View analytics, reports, and logs

## Documentation In This Repo

- [APPLICATION_DOCUMENTATION.md](./APPLICATION_DOCUMENTATION.md)
- [FEATURE_STATUS_REPORT.md](./FEATURE_STATUS_REPORT.md)
- [FULL_STACK_ECOMMERCE_PROJECT_REPORT.md](./FULL_STACK_ECOMMERCE_PROJECT_REPORT.md)
- [FULL_STACK_ECOMMERCE_PROJECT_REPORT.docx](./FULL_STACK_ECOMMERCE_PROJECT_REPORT.docx)

## Notes

- Some features depend on external credentials being configured correctly, especially `Stripe`, `Cloudinary`, social login, and SMTP email.
- Public order tracking is a real data-backed lookup flow.
- Signed-in order pages support live progress updates through Socket.IO when tracking events are emitted by the backend.

## License

This repository includes a [LICENSE](./LICENSE) file.

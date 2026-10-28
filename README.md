# 🌿 Clarity Finance

![React Native](https://img.shields.io/badge/React_Native-0.86.3-61DAFB?style=flat-square&logo=react&logoColor=black)
![Expo SDK](https://img.shields.io/badge/Expo_SDK-57-000020?style=flat-square&logo=expo&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-Strict-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Drizzle ORM](https://img.shields.io/badge/Drizzle_ORM-0.45.2-C5F74F?style=flat-square&logo=drizzle&logoColor=black)
![SQLite](https://img.shields.io/badge/SQLite-FTS5%20%2B%20SQLCipher-003B57?style=flat-square&logo=sqlite&logoColor=white)
![Bun](https://img.shields.io/badge/Bun-1.4-FBF0DF?style=flat-square&logo=bun&logoColor=black)
![React Doctor](https://img.shields.io/badge/React_Doctor-100%2F100-success?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)

> **A privacy-first, offline-first personal financial operating system.** Clarity gives you complete ownership over your financial life with zero remote tracking, local deterministic intelligence, and automated M-Pesa transaction extraction.

---

## 📑 Table of Contents

1. [Key Features](#-key-features)
2. [Architectural Principles](#-architectural-principles)
3. [Domain Map](#-domain-map)
4. [Downloads & Distribution](#-downloads--distribution)
5. [Getting Started](#-getting-started)
6. [Quality Gates & Verification](#-quality-gates--verification)
7. [Security & Privacy](#-security--privacy)
8. [Documentation Index](#-documentation-index)
9. [License](#-license)

---

## ✨ Key Features

* **100% Offline-First & Zero Telemetry**:
  All transactions, budgets, insights, and accounts are stored locally in an encrypted SQLite database using Drizzle ORM. No external servers, no third-party trackers, no telemetry, and no advertisements.
* **Automated M-Pesa & SMS Parsing**:
  Deterministic on-device regex engine automatically extracts and categorizes financial transactions (Send Money, Paybill, Buy Goods / Till, and Agent Withdrawals) directly from incoming SMS messages without transmitting message contents.
* **Safe-to-Spend & Budget Intelligence**:
  Real-time deterministic calculations calculate your daily disposable spending allowance until your next payday, accounting for active category budgets, recurring commitments, and cash flow balance.
* **Hardware-Grade Biometric Security**:
  Instant app locking with biometric authentication (Fingerprint / Face ID), persistent PIN fallback with exponential lockout backoff, and native Android `FLAG_SECURE` window protection to prevent screen captures and app-switcher snooping.
* **Complete Data Portability**:
  Export your financial ledger to standard RFC-4180 CSV spreadsheets at any time, or generate encrypted full-database backups with SHA-256 integrity checksums.

---

## 🏛️ Architectural Principles

Clarity is constructed following the **Universal Code Formatting & Architecture Standard (UCFAS)**:

* **Domain-First Organization**: Business capabilities are fully isolated into self-contained domains under `src/domains/`. Each domain encapsulates its own types, validation schemas, persistence repositories, business services, state stores, and UI views.
* **Strict App/Domain Boundary**: The `src/app/` directory is strictly reserved for Expo Router navigation file-routes. Zero business logic, data models, or direct database mutations exist within screen entry points.
* **Inward Dependency Direction**: UI components depend on domain services; domain services depend on repositories and abstractions; infrastructure and database drivers are fully replaceable.
* **Predictable Error Handling & Validation**: All domain inputs and database mutations are validated at the boundaries using Zod schemas and typed domain error classes.

---

## 🗺️ Domain Map

```
src/
├── app/                      # Expo Router navigation routes (NO business logic)
│   ├── (main)/               # Primary app tab routes (home, transactions, budget, insights)
│   ├── (onboarding)/         # First-run onboarding flow
│   └── settings/             # Sub-screens (security, backups, export, accessibility)
├── domains/                  # Isolated business capabilities
│   ├── accounts/             # Multi-account balances, account types, reconciliation
│   ├── budgeting/            # Budget allocations, safe-to-spend calculation, category limits
│   ├── identity/             # App lock, biometric auth, PIN protection, session state
│   ├── insights/             # Spending pace analysis, category dominance, local anomaly detection
│   ├── settings/             # Encrypted backup/restore, CSV export, factory reset
│   └── transactions/         # Financial pipeline, SMS parser, audit log, SQLite queries
└── shared/                   # Cross-cutting primitives
    ├── db/                   # Drizzle ORM schema, SQLite database client, migrations
    ├── i18n/                 # Dictionaries and locale management
    ├── security/             # MMKV secure key management, biometric helpers
    ├── state/                # Financial pipeline and accessibility stores
    └── ui/                   # Design system primitives (Typography, Buttons, Cards, ScreenStates)
```

---

## 📦 Downloads & Distribution

Clarity is distributed across open-source repositories and direct installation channels:

| Channel | Platform | Format | Description |
|---|---|---|---|
| **GitHub Releases** | Android | `.apk` | Download standalone signed universal APK directly from [Public Releases](https://github.com/pkaranja60/clarity-releases/releases). |
| **Obtainium** | Android | Direct Track | Add `https://github.com/pkaranja60/clarity-releases` to [Obtainium](https://github.com/ImranR98/Obtainium) for automatic background update alerts. |
| **IzzyOnDroid** | Android | F-Droid Repo | Indexed directly from GitHub Releases using Fastlane store metadata. |
| **Google Play** | Android | `.aab` | Production App Bundle submission via EAS Submit. |
| **Apple App Store**| iOS | `.ipa` | Production IPA submission via EAS Submit and TestFlight. |

For detailed publishing instructions, store guidelines, and CI/CD automation, consult the [Distribution & Release Guide](docs/DISTRIBUTION_AND_RELEASE_GUIDE.md).

---

## 🚀 Getting Started

### Prerequisites

* [Bun](https://bun.sh/) (v1.2.0 or later recommended)
* [Node.js](https://nodejs.org/) (v20 or later LTS)
* Android Studio / Xcode (only required for local native builds; Expo Go / Dev Client can be used otherwise)
* [Expo CLI](https://docs.expo.dev/) & [EAS CLI](https://docs.expo.dev/eas/)

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/pkaranja60/clarity.git
cd clarity

# 2. Install dependencies with Bun
bun install

# 3. Start the Expo development server
bun start
```

### Running on a Device or Simulator

```bash
# Android emulator or connected device
bun run android

# iOS simulator (macOS only)
bun run ios

# Web preview
bun run web
```

---

## 🧪 Quality Gates & Verification

Clarity maintains a **100% Quality Pass** baseline across all linters, compilers, and test suites:

```bash
# Run Biome linter and code style formatting check
bun run check

# Auto-fix formatting and linting issues
bun run fix

# Run strict TypeScript compiler verification
bun x tsc --noEmit

# Execute automated unit and integration tests (81 passing tests)
bun test

# Run React Doctor component architecture audit (Score: 100/100)
bun run doctor

# Run Expo Doctor configuration and dependency diagnostics (20/20 passing checks)
bun x expo-doctor
```

---

## 🛡️ Security & Privacy

* **Encrypted Storage**: Primary financial records are secured with SQLite with full FTS5 search indexing.
* **Sensitive Credentials**: Master keys and PIN salts are managed on-device via native secure hardware keystone providers.
* **Window Security**: In accordance with financial privacy standards, the app window prevents screen captures and clears the screen buffer when minimized (`FLAG_SECURE`).
* **SMS Privacy**: Incoming SMS processing executes exclusively within the device memory space. Raw SMS bodies are discarded immediately after transaction parameters are extracted.
* Full declaration: Consult the [Privacy Policy](docs/PRIVACY_POLICY.md) and [Google Play Permissions Declaration](docs/GOOGLE_PLAY_PERMISSIONS_DECLARATION.md).

---

## 📚 Documentation Index

Detailed architectural and procedural documents are located in the [docs/](docs/) directory:

* 📐 [Architecture & System Design](docs/ARCHITECTURE.md)
* 🗺️ [Domain Map](docs/DOMAIN_MAP.md)
* 📦 [Distribution & Public Release Guide](docs/DISTRIBUTION_AND_RELEASE_GUIDE.md)
* 🔒 [Privacy Policy](docs/PRIVACY_POLICY.md)
* 📱 [Google Play Permissions Declaration](docs/GOOGLE_PLAY_PERMISSIONS_DECLARATION.md)
* ⚖️ [Terms of Service](docs/TERMS_OF_SERVICE.md)
* 📊 [Market & Release Readiness Audit](docs/market_release_readiness_audit.md)

---

## 📄 License

Clarity Finance is open-source software licensed under the [MIT License](LICENSE).

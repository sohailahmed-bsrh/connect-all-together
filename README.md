# Connect All Together

## Overview
Connect All Together is a full-stack, multi-channel customer communications and CRM orchestration platform. Built on Bun and TypeScript, it integrates database migrations, consent management, automated intent classification, and multi-channel message delivery into a unified architecture.

## System Architecture

```mermaid
flowchart TD
    A[Incoming Webhooks & API Ingestion] --> B[Bun Runtime Gateway]
    B --> C[Consent & Opt-in Verification Engine]
    C --> D[Message Intent & Status Classification]
    D --> E[Drizzle ORM Persistence Layer]
    E --> F[(MySQL CRM Database)]
    E --> G[Multi-Channel Message Dispatcher]
```

## Core Features
- **Multi-Channel Dispatch**: Coordinated messaging workflows supporting SMS, email, and interactive customer messaging.
- **Consent Enforcement**: Regulatory consent tracking and audit logging to verify communication opt-ins before transmission.
- **Automated Intent Classification**: Categorization of incoming inbound communications to optimize agent routing.
- **Database Schema Migrations**: Type-safe schema definitions and automated versioned migrations powered by Drizzle ORM.

## Repository Structure
```
connect-all-together/
|-- drizzle/
|   |-- migrations/
|   |   |-- 0000_mysql_crm.sql
|   |   |-- 0002_add_consent_columns.sql
|   |   +-- 0003_add_message_status_and_intent.sql
|   +-- meta/
|-- components.json
|-- drizzle.config.ts
|-- AGENTS.md
|-- bun.lock
|-- bunfig.toml
+-- README.md
```

## Technology Stack
| Component | Technologies |
| :--- | :--- |
| Runtime | Bun |
| Language | TypeScript |
| ORM & Schema | Drizzle ORM |
| Database | MySQL |
| Validation | Zod |

## Installation & Execution
```bash
# Clone the repository
git clone https://github.com/sohailahmed-bsrh/connect-all-together.git
cd connect-all-together

# Install dependencies using Bun
bun install

# Run database migrations
bun run drizzle-kit migrate

# Start the application
bun run dev
```

## License
Distributed under the MIT License.

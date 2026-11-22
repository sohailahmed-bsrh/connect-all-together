# Connect-All-Together - Multi-Tenant Omnichannel CRM & Communications Hub

<p align="center">
  <a href="https://sohail.devsil.com"><strong>Portfolio</strong></a> | 
  <a href="https://github.com/sohailahmed-bsrh"><strong>GitHub Profile</strong></a> | 
  <a href="https://github.com/sohailahmed-bsrh/connect-all-together"><strong>Source Repository</strong></a>
</p>

---

## Executive Summary & Problem Statement

Modern businesses operate across disparate customer communication channels: WhatsApp messages, SMS notifications, email inquiries, and web forms. When customer data is siloed across isolated tools, lead response times degrade, customer history is lost, and compliance requirements regarding customer consent (such as GDPR and TCPA) become difficult to enforce.

Connect-All-Together solves this fragmentation by providing a Unified Multi-Tenant CRM and Communications Engine. Built on the high-performance Bun runtime, Drizzle ORM, and MySQL, the platform aggregates customer dialogues into a single chronological timeline, tracks granular communication consent, and coordinates automated lifecycle routing.

---

## Real-World Industry Applications

- **Omnichannel E-Commerce Support**: Unifies incoming customer inquiries from WhatsApp and web chat into a single unified dashboard with full order context.
- **Enterprise Lead Qualification**: Ingests incoming leads from marketing landing pages, enriches contact details, and assigns leads to sales reps automatically.
- **Regulatory Consent Management**: Tracks explicit opt-in timestamps, communication channels, and consent revocations to ensure compliance with privacy laws.
- **Automated Lifecycle Notifications**: Dispatches automated appointment reminders, dispatch updates, and re-engagement messaging based on customer triggers.

---

## Technical Architecture & Engineering Walkthrough

The platform couples a high-throughput webhook receiver with a type-safe relational database core:

```
[Inbound Channels: WhatsApp, SMS, Webhooks, Forms]
                          │
                          ▼
            [Bun Runtime API Gateway]
                          │
                          ▼
             [Consent Validation Engine]
       (Verifies opt-in status & channel permissions)
                          │
                          ▼
            [Customer Session Aggregator]
       (Matches phone/email to customer identity)
                          │
                          ▼
        [Drizzle ORM Relational Migration Core]
(drizzle/schema.ts & migrations/0000_mysql_crm.sql)
                          │
        ┌─────────────────┴─────────────────┐
        ▼                                   ▼
[MySQL Persistence Layer]        [Real-Time Notification Hub]
(Leads, Messages, Sessions)         (WebSockets / Server Events)
                                            │
                                            ▼
                           [Vite / React CRM Dashboard]
```

### Step 1: Omnichannel Webhook Ingestion
The Bun API gateway ingests inbound webhooks from external messaging APIs (WhatsApp Cloud API, Twilio SMS). Requests are verified for cryptographic signature authenticity before parsing payload payloads into standardized event models.

### Step 2: Customer Identity Resolution
The session tracking module parses the sender's identifier (E.164 phone number, verified email address) and queries the relational customer index. If an existing profile is found, the message is appended to the active conversation thread; otherwise, a new qualified lead record is provisioned.

### Step 3: Granular Consent Tracking
Adhering to regulatory standards, the consent engine (`drizzle/migrations/0002_add_consent_columns.sql`) evaluates opt-in state before processing outbound communications. It maintains timestamped consent logs verifying user authorization for promotional and transactional messaging.

### Step 4: Relational Persistence with Drizzle ORM
Database operations are executed through Drizzle ORM (`drizzle/schema.ts`). Schemas define type-safe relational models for accounts, contacts, leads, message sessions, message statuses, and intent classifications (`0003_add_message_status_and_intent.sql`).

### Step 5: Real-Time Collaborative CRM Interface
The frontend provides a real-time reactive workspace where customer support agents and account executives view unified message histories, update pipeline stages, and trigger automated multi-channel responses.

---

## Technology Stack & Implementation Specifications

| Component | Technology | Version | Architectural Function |
| :--- | :--- | :--- | :--- |
| **Server Runtime** | Bun Runtime | Latest | High-throughput JavaScript execution and package manager |
| **Language & Typing** | TypeScript | 5.x | Strict end-to-end type safety across client and server |
| **ORM & Migrations** | Drizzle ORM | 0.30+ | Declarative schema definitions and automated SQL migrations |
| **Database Engine** | MySQL / Supabase | 8.0+ | ACID-compliant relational data persistence |
| **Frontend Client** | Vite / React.js | 18.x | Fast component rendering and real-time interface |
| **UI Components** | Tailwind CSS / Radix UI | Latest | Accessible, responsive, modern CRM styling |
| **Linting & Code Quality** | ESLint / Prettier | Latest | Code standardization and quality assurance |

---

## Database Migration & Setup Guide

### 1. Configure Environment
Create a `.env` file:
```env
DATABASE_URL=mysql://user:password@localhost:3306/connect_crm
PORT=3000
```

### 2. Execute Migrations & Start
```bash
bun install

# Run database schema migrations:
bun run drizzle-kit generate:mysql
bun run drizzle-kit push:mysql

# Launch development server:
bun run dev
```

---

## Author & Contact Information

<table width="100%">
  <tr>
    <td width="150" align="center" valign="middle">
      <img src="https://avatars.githubusercontent.com/u/231165170?v=4" width="120" style="border-radius: 50%;" alt="Sohail Ahmed"/>
    </td>
    <td>
      <h3>Sohail Ahmed</h3>
      <p><strong>Senior Software Engineer & AI Systems Architect</strong></p>
      <p>Specializing in Full-Stack AI Application Development, Computer Vision, Deep Learning Pipelines, and Scalable Automation Architectures.</p>
      <p>
        <a href="https://sohail.devsil.com"><strong>Portfolio Website</strong></a> | 
        <a href="https://github.com/sohailahmed-bsrh"><strong>GitHub Profile</strong></a> | 
        <a href="https://www.linkedin.com/in/sohail-ahmed-devsil/"><strong>LinkedIn</strong></a> | 
        <a href="https://www.kaggle.com/sohail2411126"><strong>Kaggle</strong></a> | 
        <a href="https://x.com/ahmed241126"><strong>Twitter/X</strong></a> | 
        <a href="mailto:se906403@gmail.com"><strong>Email Contact</strong></a>
      </p>
    </td>
  </tr>
</table>

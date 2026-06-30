# Miriam Karimi

Backend engineer with a background in building and maintaining APIs within a microservices architecture, primarily using NestJS and TypeScript, with deployment and operations experience on Kubernetes. My work has centered on the payments domain  designing how services communicate, handle failure, and stay consistent under real production conditions.

I'm currently deepening my focus on systems-level engineering: architecture decisions, operational reliability, and the workflow discipline that holds a distributed system together once it's live, not just when it's first shipped.

## Current project M-Pesa Integration

A production grade integration with Safaricom's Daraja API, built end-to-end.

**What it does**
Accepts payments from customers via STK Push and Paybill (C2B), and disburses payments to customers and partner businesses via B2C and B2B the full money-in, money-out cycle that a real fintech product needs.

**How it's engineered**
M-Pesa communicates asynchronously: your server gets an immediate acknowledgment, then the real result arrives later as a webhook callback, sometimes more than once, sometimes not at all. The system is built around that reality rather than around the happy path:

- A transaction ledger with an explicit state machine (initiated → pending → success/failed/cancelled), so the database — not the UI — is always the source of truth
- Idempotent webhook handling, keyed on Safaricom's own request identifiers, so duplicate callbacks can't double-credit a payment
- A nightly reconciliation job that queries M-Pesa directly for any transaction that never received a callback, so nothing silently falls through
- Secrets and credentials isolated server-side, never exposed to the client

**Stack**
Node.js, TypeScript, PostgreSQL, deployed to production with CI/CD.

**Status**
In active development — repo and live demo linked here once Phase 1 is complete.

`github.com/karimimiriam/mpesa-integration` *(coming soon)*

**Connect:** [LinkedIn or X — your call]

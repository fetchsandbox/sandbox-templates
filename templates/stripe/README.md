# Stripe API Template

Full Stripe Connect + Payments sandbox with 40+ endpoints covering accounts, charges, disputes, capabilities, billing, and more.

## Resources & State Machines

| Resource | States | Key Transitions |
|----------|--------|-----------------|
| Accounts | onboarding → active → restricted → disabled | Onboarding flow with verification gates |
| Charges | pending → succeeded / failed | Payment capture and decline flows |
| Disputes | needs_response → under_review → won / lost | Full chargeback lifecycle |
| Capabilities | unrequested → pending → active / disabled | Verification-gated enablement |
| External Accounts | new → validated → verified / errored | Bank account verification |

## Scenarios

| Scenario | Description |
|----------|-------------|
| `default` | Happy path — all operations succeed |
| `auth_failure` | Invalid API key (401) |
| `rate_limited` | Too many requests (429) |
| `payment_declined` | Card declined by issuer (402) |
| `insufficient_funds` | Not enough balance (402) |
| `fraud_hold` | Radar flags payment as fraudulent |
| `processing_error` | Stripe infrastructure error (500) |
| `account_onboarding_failure` | Identity verification fails |
| `dispute_escalation` | Lost dispute, blocked refunds |

## Seed Data

- 3 connected accounts (US express, UK standard, DE custom)
- 3 charges (succeeded, failed, refunded)
- 3 disputes (needs_response, under_review, won)
- Bank accounts, capabilities, persons, billing meters, and more

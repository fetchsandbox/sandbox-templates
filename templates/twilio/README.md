# Twilio Messaging API Template

SMS/MMS messaging sandbox with message lifecycle tracking, phone number management, and messaging services.

## Resources & State Machines

| Resource | States | Key Transitions |
|----------|--------|-----------------|
| Messages | queued → sending → sent → delivered / undelivered / failed | Full delivery lifecycle with branching outcomes |
| Phone Numbers | in-use → released | Provision and release numbers |
| Messaging Services | active ↔ suspended | Service management |

## Scenarios

| Scenario | Description |
|----------|-------------|
| `default` | Messages deliver successfully |
| `auth_failure` | Invalid credentials (401) |
| `rate_limited` | Too many requests (429) |
| `message_undeliverable` | Carrier rejects delivery (error 30003) |
| `invalid_number` | Bad destination number (400) |
| `queue_overflow` | Messages stuck in queued state |
| `international_blocked` | Geo-permissions deny international SMS (403) |

## Seed Data

- 3 messages (verification code delivered, shipping notification sent, inbound STOP)
- 3 phone numbers (main SMS, marketing, toll-free support)
- 3 messaging services (transactional, marketing, 2FA)
- 3 usage records (SMS, MMS, phone numbers)

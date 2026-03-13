# Sandbox Templates

Ready-to-use API sandbox templates for [FetchSandbox](https://fetchsandbox.com). Each template includes everything needed to spin up a fully functional API sandbox — OpenAPI spec, state machine config, realistic seed data, and pre-built error scenarios.

## Templates

| Template | API Type | Endpoints | States | Scenarios |
|----------|----------|-----------|--------|-----------|
| [Stripe](templates/stripe/) | Payments & Connect | 40+ | Charges, disputes, accounts, capabilities | Payment declined, fraud hold, rate limited |
| [Twilio](templates/twilio/) | Messaging (SMS/MMS) | 12 | Messages (queued → delivered), phone numbers | Carrier rejection, invalid number, geo-blocked |
| [GitHub](templates/github/) | Developer Tools | 16 | Repos, issues, pull requests | Rate limited, merge conflict, read-only token |

## Template Structure

Each template contains 4 files:

```
templates/<api>/
├── openapi.yaml         # OpenAPI 3.0 spec defining all endpoints
├── sandbox_config.yaml  # State machines, auth mode, webhook events
├── seed_data.yaml       # Realistic initial records
└── scenarios.yaml       # Pre-built error/edge-case scenarios
```

### openapi.yaml
Standard OpenAPI 3.0.3 specification. Defines paths, request/response schemas, and operation IDs that the sandbox engine uses for routing.

### sandbox_config.yaml
Defines how the sandbox behaves:
- **resources** — Each resource type with its states and valid transitions (e.g., a message goes `queued → sending → sent → delivered`)
- **auth** — Authentication mode (`relaxed` accepts any token, `strict` validates against credentials)
- **webhooks** — Events the sandbox can fire (e.g., `message.delivered`, `charge.succeeded`)

### seed_data.yaml
Pre-populated records so the sandbox feels real from the first API call. Includes realistic names, amounts, timestamps, and cross-references between resources.

### scenarios.yaml
Named configurations that override default behavior to simulate edge cases:
- `auth_failure` — All requests return 401
- `rate_limited` — All requests return 429
- API-specific scenarios like `payment_declined`, `message_undeliverable`, `merge_conflict`

## Usage

### On FetchSandbox
Upload your OpenAPI spec at [fetchsandbox.com](https://fetchsandbox.com) and the platform auto-generates a sandbox with state machines, seed data, and scenarios.

### Self-hosted
Copy a template directory into your FetchSandbox backend:

```bash
# Spec goes in backend/specs/<api>/
cp templates/twilio/openapi.yaml backend/specs/twilio/openapi.yaml

# Config files go in backend/configs/<api>/
cp templates/twilio/sandbox_config.yaml backend/configs/twilio/sandbox_config.yaml
cp templates/twilio/seed_data.yaml backend/configs/twilio/seed_data.yaml
cp templates/twilio/scenarios.yaml backend/configs/twilio/scenarios.yaml
```

## Contributing

Want to add a template for an API you use? Follow the structure above and submit a PR. Good candidates:
- PagerDuty (incident management)
- SendGrid (email delivery)
- Slack (messaging platform)
- Shopify (e-commerce)
- Plaid (banking/fintech)

## License

MIT

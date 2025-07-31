# BillingOps Manager

> **Smart Stripe Subscription Automation with n8n + Airtable**

BillingOps Manager is a resource-efficient, production-grade automation system built with n8n, Airtable, and Stripe. It captures subscription events in real time, updates your CRM records, and logs changes to a history table.

Perfect for SaaS startups, no-code entrepreneurs, and agencies needing a streamlined billing system without writing code.

---

## 🔧 Tech Stack

- **Stripe** – for handling checkout and subscription events
- **n8n** – for automation logic and API communication
- **Airtable** – as a CRM + logging backend

---

## ✨ Features

- 🔁 Real-time sync of Stripe subscriptions to Airtable
- 📥 Handles:
  - `checkout.session.completed`
  - `customer.subscription.updated`
- 🗂 Upserts customer data into `subscriptions` table
- 📝 Tracks changes in `subscription history`
- 🧠 Lightweight: No unnecessary HTTP requests
- 🔐 Supports Stripe's single-subscription restriction (optional)
- 🚀 Ready for deployment (Docker, Cloud, or local n8n)

---

## ⚙️ Requirements

- Stripe account with subscriptions enabled
- Airtable base with two tables:
  - `subscriptions`
  - `subscription history`
- n8n instance (self-hosted or cloud)
- Airtable Personal Access Token
- Stripe API Secret Key (test or live)

---

## 🧱 Airtable Schema

### `subscriptions` Table
Stores the current status of each active subscription.

| Field Name              | Type       | Description                        |
|------------------------|------------|------------------------------------|
| subscription_id        | String     | Stripe Subscription ID             |
| customer_id            | String     | Stripe Customer ID                 |
| Name                   | String     | Customer name                      |
| Email                  | String     | Customer email                     |
| Plan                   | Option     | Basic / Silver / Gold              |
| Frequency              | Option     | Daily / Monthly / Yearly           |
| amount_total           | Number     | Total payment amount (USD)         |
| Status                 | Option     | active / canceled / past_due...    |
| session_id             | String     | Checkout session ID                |
| created_at             | DateTime   | Subscription creation date         |
| start_date             | DateTime   | Start of billing cycle             |
| end_date               | DateTime   | End of billing cycle               |
| cancel_at_period_end   | Boolean    | Cancellation scheduled?            |
| last_updated_at        | DateTime   | Last time this record was updated  |
| event_type             | String     | Event source (checkout, update)    |
| Subscription History   | Link       | Linked to history table (optional) |

### `subscription history` Table
Tracks every change (plan switch, amount update, etc.) for auditing and customer support.

| Field Name           | Type     | Description                          |
|---------------------|----------|--------------------------------------|
| customer_id         | String   | Stripe Customer ID                   |
| subscription_id     | String   | Stripe Subscription ID               |
| Email               | String   | Customer email                       |
| event_type          | String   | Event type that triggered logging    |
| from_plan           | String   | Previous plan (if any)               |
| to_plan             | String   | New plan                             |
| from_amount         | Number   | Previous billing amount              |
| to_amount           | Number   | New billing amount                   |
| credit_or_charge    | Number   | Amount adjusted (if applicable)      |
| prorated            | Boolean  | Was the change prorated?             |
| timestamp           | DateTime | When the change occurred             |
| Notes               | String   | Additional context or admin notes    |
| Subscription Record | Link     | Linked to the subscription row       |

---

## 🚀 Deployment

### 1. Clone or Import Workflow
- Import `stripe-subscription-workflow.json` into your n8n instance.

### 2. Configure Webhook
- Copy the webhook URL from Stripe Trigger node
- Paste it into Stripe > Developers > Webhooks
- Events to enable:
  - `checkout.session.completed`
  - `customer.subscription.updated`

### 3. Set Environment Variables or Credentials
- Create credentials for:
  - Airtable Token API
  - Stripe API (test/live)

---

## 📦 Future Improvements

- Add automatic invoice/receipt email
- Include failed payment retries
- Extend support to multi-product subscriptions
- Add customer portal integration

---

## 👥 Who Should Use This?

- SaaS founders managing subscription logic
- No-code builders needing Stripe-to-CRM sync
- Freelancers offering Stripe automation as a service

---

## 📣 License

MIT License — use it freely for commercial or personal projects.

---

## 🤝 Credits

Built with ❤️ using:
- [n8n](https://n8n.io)
- [Stripe](https://stripe.com)
- [Airtable](https://airtable.com)

---

## 📬 Questions or Issues?
Reach out via GitHub issues or Upwork/Fiverr gigs!


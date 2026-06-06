# 🛍️ ShopFlow — AI-Powered E-commerce Automation System

> Built with n8n | OpenAI | Google Sheets | Gmail | Slack | Telegram

---

## 📌 Overview

ShopFlow is a fully automated order management system that classifies customers using AI, sends personalized emails, logs everything to a live CRM dashboard, and alerts the team via Slack — all triggered by a single Shopify webhook.

**Zero manual work. Real-time. Bulletproof.**

---

## 🎯 The Problem

E-commerce businesses waste hours every day on repetitive tasks:
- Manually checking new orders
- Copying customer data into spreadsheets
- Sending the same confirmation emails
- Notifying the team about new orders
- Trying to figure out which customers are VIPs

Most businesses either do this manually or pay for expensive SaaS tools that don't talk to each other.

---

## ✅ The Solution

ShopFlow automates the entire post-order workflow in seconds:

1. **New order arrives** via Shopify webhook
2. **AI classifies the customer** as New, Returning, or VIP
3. **Personalized email sent** based on customer segment
4. **CRM automatically updated** across 3 organized sheets
5. **Team notified** instantly via Slack
6. **Errors caught and alerted** via Slack + Telegram

---

## 🔄 Workflow Architecture

```
Shopify Order (Webhook)
        ↓
OpenAI — AI Customer Classification
        ↓
Edit Fields — Data Cleaning & Structuring
        ↓
IF Node — Data Validation
   ↓ Valid              ↓ Invalid
Switch Node         Stop and Error
↙    ↓    ↘              ↓
New Return VIP     Error Handler
   ↘   ↓   ↙      Slack + Telegram
   Gmail x3
      ↓
Google Sheets: Customers
      ↓
Google Sheets: Orders
      ↓
Google Sheets: Email History
      ↓
Slack: Team Notification
```

---

## 🤖 AI Classification Logic

| Segment | Criteria | Email Treatment |
|---|---|---|
| **NEW** | orders_count ≤ 1 | Welcome email + 10% discount code |
| **RETURNING** | orders_count 2–4 | Thank you email + 15% discount code |
| **VIP** | orders_count ≥ 5 OR total_spent > $2,000 | VIP email + 20% off + free shipping |

---

## 📊 CRM Dashboard (Google Sheets)

Automatically maintained across 4 tabs:

| Tab | Contents |
|---|---|
| **Dashboard** | Live metrics — total customers, revenue, emails sent |
| **Customers** | Customer ID, name, email, segment, total spent |
| **Orders** | Order ID, product, total, date, status |
| **Email History** | Date, segment, subject, delivery status |

Dashboard metrics auto-update via Google Sheets formulas every time n8n writes new data.

---

## 🛡️ Error Handling (3 Layers)

### Layer 1 — Data Validation (IF + Stop and Error)
Rejects orders with missing name or email before they reach the AI or Gmail nodes.

### Layer 2 — AI Protection (Continue on Error)
If OpenAI fails, the workflow catches the error and sends a Slack alert for manual review instead of crashing.

### Layer 3 — Error Trigger Workflow
A separate background workflow monitors ShopFlow 24/7. Any unexpected crash triggers instant alerts to both Slack and Telegram with:
- Workflow name
- Failed node
- Error message
- Timestamp

---

## 🧰 Tech Stack

| Tool | Purpose |
|---|---|
| **n8n** | Workflow automation platform |
| **OpenAI GPT-4o-mini** | Customer classification |
| **Gmail** | Personalized transactional emails |
| **Google Sheets** | CRM database + live dashboard |
| **Slack** | Team notifications + error alerts |
| **Telegram** | Backup error alerts |
| **Hoppscotch** | Webhook testing (Shopify simulation) |

---

## 📁 Files in This Repository

```
shopflow-automation/
├── README.md
├── workflows/
│   ├── ShopFlow_Automation.json
│   └── ShopFlow_Error_Handler.json
└── screenshots/
    ├── canvas.png
    ├── crm-dashboard.png
    ├── customers-sheet.png
    ├── orders-sheet.png
    ├── email-history-sheet.png
    ├── slack-notification.png
    └── error-alert.png
```

---

## 🚀 How to Deploy

1. Import `ShopFlow_Automation.json` into your n8n instance
2. Import `ShopFlow_Error_Handler.json` into n8n
3. Connect credentials: OpenAI, Gmail, Google Sheets, Slack, Telegram
4. Update Google Sheets ID in all 3 Sheets nodes
5. Link Error Handler in ShopFlow Settings → Error Workflow
6. Publish both workflows
7. Connect Shopify webhook to your production webhook URL

---

## 💼 Business Value

| Metric | Impact |
|---|---|
| Time saved | 2–3 hours/day of manual work eliminated |
| Response time | Instant vs. manual (hours/days) |
| Personalization | 3 targeted email types vs. generic confirmation |
| Visibility | Live CRM dashboard vs. scattered data |
| Reliability | Triple-layer error handling vs. silent failures |

---

## 👩‍💻 Built By

**Alieza San Diego** — n8n Automation Specialist

Specializing in AI-powered workflow automation for e-commerce and service businesses.

---

*Built with n8n — the most powerful open-source automation platform.*

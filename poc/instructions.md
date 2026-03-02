The end goal is to build a **SaaS business** — the app itself is just the vehicle.

Here's how to think about it in layers:

---

**Layer 1 — The POC (where you start)**
A simple 3-screen lead tracker for small restaurants and retail shops in Venezuela. Cheap to build, cheap to run, easy to sell. Its only job is to **validate that people will pay for it.**

---

**Layer 2 — The Product (months 3-12)**
Once validated, you expand it into a proper CRM — adding contact history, WhatsApp integration, basic reporting, invoicing. You charge **$29-$79/month per business.** At 50 clients that's **~$2,000/month recurring** with almost no infrastructure cost.

---

**Layer 3 — The Platform (year 2+)**
The CRM becomes the foundation of a broader digital services platform. You add modules — inventory, appointments, loyalty programs — and sell them as upgrades. You also white-label the platform to **sell to other developers or agencies** in Venezuela and neighboring markets like Colombia and Ecuador.

---

**The Real Business**

```
POC  →  Validated product  →  Recurring revenue  →  Fundable company
```

The app is not the goal. The goal is to build a **predictable, recurring revenue stream** that:

- Runs on near-zero infrastructure cost (serverless)
- Scales without hiring proportionally
- Can be sold to investors as a regional SaaS play
- Leverages your enterprise engineering background to deliver quality that local competitors simply can't match

---

**Why start with restaurants and retail?**

Because they are the **fastest path to a paying customer.** A restaurant owner in Caracas understands immediately why tracking leads and follow-ups matters — they lose business every day because of disorganization. The pain is obvious, the sale is short, and word of mouth within that community is fast.

They are not the only customer forever — they are your **beachhead market** to prove the model works before expanding to hospitality, professional services, and beyond.

---

In short: you're not building a lead tracker. You're building a company that starts with a lead tracker because it's the simplest possible thing that generates real revenue fast. Does that framing make sense?

----

Good choices. Here's my recommendation for the backend, and then the full picture:

**For backend: AWS Lambda + Function URLs** — here's why:
- No API Gateway cost (saves ~$3.50 per million requests)
- Go runs extremely well on Lambda (fast cold starts, low memory)
- Stays within AWS ecosystem alongside your long-term plan
- Function URLs give you a direct HTTPS endpoint, zero extra config

---

**Your Full Stack Decision**

| Layer | Technology | Monthly Cost (0-10 clients) |
|---|---|---|
| Frontend | Next.js on Vercel | **$0** (free tier) |
| Backend | Go on AWS Lambda + Function URLs | **~$0** (1M requests free/month) |
| Database | PlanetScale (MySQL) | **$0** (free tier: 5GB, 1B reads) |
| Auth | Supabase Auth only | **$0** (free tier) |
| Storage | AWS S3 | **~$0.02** |
| Domain | Namecheap or Cloudflare | **~$1/mo** |
| **Total** | | **~$1/month** |

At 100 clients you're still under **$30/month**. That's the power of serverless at this scale.

---

**Architecture Diagram**

```
[User Browser]
      │
      ▼
[Vercel — Next.js Frontend]
      │  HTTPS
      ▼
[AWS Lambda — Go API]  ←──→  [PlanetScale — MySQL]
      │
      ▼
[Supabase — Auth/JWT validation]
```

---

**Clean Architecture in Go for Lambda**

Your Lambda function follows the same clean architecture structure, just with a Lambda handler as the entry point instead of an HTTP server:

```
/cmd
  /lambda          → Lambda handler (entry point)
/internal
  /domain          → Lead, Contact, Pipeline entities
  /usecase         → CreateLead, MovePipeline, GetContacts
  /interface
    /handler       → HTTP handlers (Lambda-compatible)
  /infrastructure
    /mysql         → PlanetScale repository implementations
    /auth          → Supabase JWT validation
/pkg
  /response        → Standard API response helpers
```

---

**The 3 Screens — Exact Scope**

**Screen 1 — Contacts List**
- Table: Name, Phone, Business, Stage, Last Updated
- Search bar (filter by name or business)
- "Add Contact" button → Screen 3
- WhatsApp icon per row → opens `wa.me/{phone}`

**Screen 2 — Pipeline Board (Kanban)**
- 4 columns: `Nuevo` → `Contactado` → `Interesado` → `Cerrado`
- Drag-and-drop card between columns
- Each card: name, business, phone
- Click card → opens edit form

**Screen 3 — Add / Edit Contact Form**
- Fields: Name, Phone, Business name, Notes, Stage (dropdown)
- Save / Cancel buttons
- Delete button (edit mode only)

That's the entire POC. No login complexity, no billing, no settings — just the core loop.

---

**Estimated Build Timeline**

| Week | Work |
|---|---|
| 1 | Go Lambda setup, PlanetScale schema, deploy pipeline (CI/CD) |
| 2 | API endpoints: CRUD contacts + pipeline stage update |
| 3 | Next.js frontend: Screen 1 + Screen 3 |
| 4 | Screen 2 (Kanban), WhatsApp button, polish |
| 5 | Auth (Supabase), multi-tenant (one DB per business) |
| 6 | Testing with 2-3 pilot restaurants, gather feedback |

---

Ready to go deeper on any of these? I can help you with the Go Lambda project structure and first endpoints, the PlanetScale schema design for the CRM, the Next.js component structure, or the Vercel + AWS deployment pipeline.

Where do you want to start?
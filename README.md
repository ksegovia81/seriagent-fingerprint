# SeriAgent by Fingerprint 🖨️

> An intelligent AI assistant for screen printing management, built for the Oracle ONE AI Immersion Program 2026.

---

## What is SeriAgent?

SeriAgent is a full-stack web application built with **Oracle APEX** that helps screen printing studios in Paraguay manage orders, troubleshoot technical issues, and answer client questions — all powered by **OCI Generative AI** and **Oracle AI Vector Search**.

This project was developed by **Katherine J.** as part of the **Oracle ONE AI Immersion Program (May 2026)**, focused on **Agentic AI** applied to a real small business context.

**Business:** [Fingerprint](https://fingerprint.com.py) — a premium serigraphy studio in Asunción, Paraguay.

---

## The Problem It Solves

Small screen printing businesses spend significant time:
- Answering repetitive technical questions (mesh counts, ink types, curing temperatures)
- Manually tracking orders across clients like Murillo Autoservicio
- Generating quotes and managing material inventory

SeriAgent automates and intelligently assists with all three.

---

## Features

| Feature | Technology | Status |
|---|---|---|
| Order Management Dashboard | Oracle APEX + Autonomous DB | ✅ Built |
| Client & Materials Tracking | Oracle APEX + SQL | ✅ Built |
| AI Technical Troubleshooter | OCI Generative AI (RAG) | 🔧 In Progress |
| "Chat with your Manuals" | Oracle AI Vector Search | 🔧 In Progress |
| Bilingual Support (ES/EN) | APEX Globalization | ✅ Built |
| Cost & Quote Generator | PL/SQL + APEX Forms | 🔧 In Progress |

---

## Tech Stack

- **Frontend:** Oracle APEX 24.2 (Low-code, Progressive Web App enabled)
- **Database:** Oracle Autonomous Database (Always Free Tier)
- **AI Layer:** OCI Generative AI — Llama 3 / Command R+
- **Knowledge Base:** Oracle AI Vector Search (RAG pipeline)
- **Cloud:** Oracle Cloud Infrastructure (OCI) — Always Free

---

## Database Schema

```sql
-- Orders table
FINGERPRINT_ORDERS (id, client_name, project_name, product_type, quantity, ink_colors, status, order_date)

-- Clients table
FINGERPRINT_CLIENTS (id, client_name, contact_name, phone, email, city, notes, created_date)

-- Materials/Inventory table
FINGERPRINT_MATERIALS (id, material_name, category, unit, stock_quantity, reorder_level, unit_cost, supplier, last_updated)

-- Knowledge Base table (for RAG)
FINGERPRINT_KNOWLEDGE (id, doc_title, category, content_text, source_file, date_added)
```

---

## Project Structure

```
seriagent-fingerprint/
│
├── sql/
│   ├── 01_create_tables.sql       # Full schema setup
│   └── 02_sample_data.sql         # Test data (Murillo Autoservicio, Lumen School)
│
├── apex/
│   └── seriagent_export.sql       # APEX application export
│
├── prompts/
│   └── system_prompt.md           # SeriBot AI system prompt
│
└── README.md
```

---

## AI System Prompt (SeriBot Personality)

SeriBot is configured as a **bilingual (ES/EN) technical expert** for screen printing. It:
- Responds in the user's language automatically
- Provides exact technical values (mesh counts, curing temps, exposure times)
- Uses local Paraguayan serigraphy terminology
- Searches uploaded technical manuals before answering (RAG)
- Reminds users of safety practices (ventilation, heat)

See full prompt: [`/prompts/system_prompt.md`](./prompts/system_prompt.md)

---

## How to Run This Project

### Option 1: Oracle APEX Sandbox (No AI features)
1. Go to [apex.oracle.com](https://apex.oracle.com) and request a free workspace
2. In **SQL Workshop > SQL Scripts**, run `sql/01_create_tables.sql`, then `sql/02_sample_data.sql`
3. In **App Builder**, import `apex/seriagent_export.sql`

### Option 2: OCI Always Free (Full AI features)
1. Create a free account at [oracle.com/cloud/free](https://oracle.com/cloud/free)
2. Provision an **Autonomous Database**
3. Enable **APEX** and **OCI Generative AI** in your tenancy
4. Follow the same import steps above
5. In **Workspace Utilities > Generative AI**, configure your OCI credentials

---

## About the Developer

**Katherine J.** is an ELA/ESL teacher at Lumen School, Asunción, Paraguay, with 30 years of classroom experience and a growing screen printing business called **Fingerprint**, with a social-impact sub-brand **Heñói**.

This project connects her experience in education technology, content creation, and small business ownership into a single practical AI solution.

---

## Oracle ONE Program Context

- **Program:** Oracle Next Education (ONE) — AI Immersion 2026
- **Focus:** Agentic AI with Oracle APEX + OCI Generative AI
- **Immersion Dates:** May 18–22, 2026
- **Track:** Full Stack Low-Code with Intelligent Agents

---

*Built with ☕ and ink in Asunción, Paraguay.*

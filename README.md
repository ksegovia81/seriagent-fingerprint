# SeriAgent by Fingerprint 🖨️

📄 [Versión en Español](./README.es.md)

> An intelligent AI assistant for screen printing management, built for the Oracle ONE AI Immersion Program 2026.

---

## What is SeriAgent?

SeriAgent is a full-stack web application that helps screen printing studios in Paraguay manage orders, troubleshoot technical issues, and answer client questions — powered by **n8n**, **Cohere**, and **Oracle APEX**.

This project was developed by **Katherine S.** as part of the **Oracle ONE AI Immersion Program (May 2026)**, focused on **Agentic AI** applied to a real small business context.

**Business:** Fingerprint — a premium serigraphy studio in Asunción, Paraguay.
**Slogan:** *Impresiones que dejan huella*

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
| Order Management Dashboard | Oracle APEX + Autonomous DB | ✅ Live |
| Client & Materials Tracking | Oracle APEX + SQL | ✅ Live |
| AI Technical Troubleshooter | n8n + Cohere + Vector Store | ✅ Live |
| "Chat with your Manuals" (RAG) | n8n RAG Flow + Cohere Embeddings | ✅ Live |
| Bilingual Support (ES/EN) | APEX Globalization + Cohere | ✅ Live |
| Cost & Quote Generator | SeriAgent Chat (Cohere) | ✅ Live |

---

## Tech Stack

- **Frontend:** Oracle APEX 24.2 (Low-code, Progressive Web App enabled)
- **Database:** Oracle Autonomous Database (Always Free Tier)
- **AI Agent:** n8n Cloud + Cohere Command R
- **Vector Store:** n8n Simple Vector Store (RAG pipeline)
- **Embeddings:** Cohere Embeddings
- **Knowledge Base:** 12 technical entries including official Saati Hi-R Mesh data (Oct 2024)
- **Cloud:** Oracle Cloud Infrastructure (OCI) — Always Free — US East (Ashburn)

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
│   ├── seriagent_full_setup.sql          # Full schema + sample data
│   ├── seriagent_knowledge_base.sql      # 12 AI knowledge entries
│   └── seriagent_saati_exposure.sql      # Saati mesh + exposure data
│
├── n8n/
│   ├── SeriAgent_Flow1_BasesDatos.json   # n8n Vector Store loader
│   └── SeriAgent_Flow2_Chat.json         # n8n AI Agent chat flow
│
├── knowledge/
│   └── SeriAgent_Knowledge_Base.txt      # RAG knowledge document
│
├── README.md                             # English version
└── README.es.md                          # Spanish version
```

---

## How the AI Agent Works

**Flow 1 — Knowledge Loader:**
1. HTTP Request fetches `SeriAgent_Knowledge_Base.txt` from GitHub
2. Cohere Embeddings converts the text into vectors
3. Simple Vector Store saves the vectors for semantic search

**Flow 2 — Chat Agent:**
1. User sends a message via chat
2. AI Agent searches the Vector Store for relevant knowledge
3. Cohere Command R generates a precise, contextual answer
4. Simple Memory maintains conversation context

**Example interactions:**
- *"¿Qué malla uso para bolsas tote canvas oscuras?"* → Recommends mesh 110 for base, 150-158 for top colors
- *"¿Cuánto cuestan 50 bolsas con 2 colores?"* → Calculates Gs. 2,250,000 automatically
- *"La tinta se lava después del primer lavado"* → Diagnoses incomplete cure, gives exact temperatures

---

## How to Run This Project

### Option 1: Oracle APEX (Database + Dashboard)
1. Go to [apex.oracle.com](https://apex.oracle.com) and request a free workspace
2. In **SQL Workshop > SQL Scripts**, run `sql/seriagent_full_setup.sql`
3. In **App Builder**, create a new app from the `FINGERPRINT_ORDERS` table

### Option 2: n8n + Cohere (AI Agent)
1. Create a free account at [n8n.io](https://n8n.io)
2. Import `n8n/SeriAgent_Flow1_BasesDatos.json`
3. Import `n8n/SeriAgent_Flow2_Chat.json`
4. Add your **Cohere API key** in both flows
5. Execute Flow 1 to load the knowledge base
6. Open the chat in Flow 2 and start asking questions

---

## About the Developer

**Katherine S.** is an ELA/ESL teacher at Lumen School, Asunción, Paraguay, with 30 years of classroom experience and a growing screen printing business called **Fingerprint**, with a social-impact sub-brand **Heñói**.

This project connects her experience in education technology, content creation, and small business ownership into a single practical AI solution.

---

## Oracle ONE Program Context

- **Program:** Oracle Next Education (ONE) — AI Immersion 2026
- **Focus:** Agentic AI with n8n + Cohere + Oracle APEX
- **Immersion Dates:** May 18–22, 2026
- **Track:** Full Stack Low-Code with Intelligent Agents

---

*Built with ☕ and ink in Asunción, Paraguay.*

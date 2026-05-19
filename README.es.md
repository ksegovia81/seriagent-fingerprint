# SeriAgent by Fingerprint 🖨️

📄 [English Version](./README.md)

> Un asistente de inteligencia artificial para la gestión de serigrafía, desarrollado para el Programa de Inmersión en IA de Oracle ONE 2026.

---

## ¿Qué es SeriAgent?

SeriAgent es una aplicación web full stack que ayuda a los talleres de serigrafía en Paraguay a gestionar pedidos, resolver problemas técnicos y responder consultas de clientes — impulsada por **n8n**, **Cohere** y **Oracle APEX**.

Este proyecto fue desarrollado por **Katherine S.** como parte del **Programa de Inmersión en IA de Oracle ONE (mayo 2026)**, con enfoque en **Agentes de IA** aplicados a un negocio real.

**Negocio:** Fingerprint — estudio premium de serigrafía en Asunción, Paraguay.
**Slogan:** *Impresiones que dejan huella*

---

## El Problema que Resuelve

Los talleres de serigrafía pequeños dedican mucho tiempo a:
- Responder preguntas técnicas repetitivas (conteo de mallas, tipos de tinta, temperaturas de curado)
- Hacer seguimiento manual de pedidos de clientes como Murillo Autoservicio
- Generar cotizaciones y administrar el inventario de materiales

SeriAgent automatiza y asiste de forma inteligente en los tres aspectos.

---

## Funcionalidades

| Funcionalidad | Tecnología | Estado |
|---|---|---|
| Panel de Gestión de Pedidos | Oracle APEX + Autonomous DB | ✅ En vivo |
| Seguimiento de Clientes y Materiales | Oracle APEX + SQL | ✅ En vivo |
| Asistente Técnico con IA | n8n + Cohere + Vector Store | ✅ En vivo |
| "Consultá tus Manuales" (RAG) | n8n RAG Flow + Cohere Embeddings | ✅ En vivo |
| Soporte Bilingüe (ES/EN) | Globalización APEX + Cohere | ✅ En vivo |
| Generador de Cotizaciones | SeriAgent Chat (Cohere) | ✅ En vivo |

---

## Stack Tecnológico

- **Frontend:** Oracle APEX 24.2 (Low-code, con soporte para Progressive Web App)
- **Base de datos:** Oracle Autonomous Database (Nivel Always Free)
- **Agente de IA:** n8n Cloud + Cohere Command R
- **Vector Store:** n8n Simple Vector Store (pipeline RAG)
- **Embeddings:** Cohere Embeddings
- **Base de Conocimiento:** 12 entradas técnicas incluyendo datos oficiales Saati Hi-R Mesh (Oct 2024)
- **Nube:** Oracle Cloud Infrastructure (OCI) — Always Free — US East (Ashburn)

---

## Esquema de Base de Datos

```sql
-- Tabla de pedidos
FINGERPRINT_ORDERS (id, client_name, project_name, product_type, quantity, ink_colors, status, order_date)

-- Tabla de clientes
FINGERPRINT_CLIENTS (id, client_name, contact_name, phone, email, city, notes, created_date)

-- Tabla de materiales / inventario
FINGERPRINT_MATERIALS (id, material_name, category, unit, stock_quantity, reorder_level, unit_cost, supplier, last_updated)

-- Tabla de base de conocimiento (para RAG)
FINGERPRINT_KNOWLEDGE (id, doc_title, category, content_text, source_file, date_added)
```

---

## Estructura del Proyecto

```
seriagent-fingerprint/
│
├── sql/
│   ├── seriagent_full_setup.sql          # Esquema completo + datos de prueba
│   ├── seriagent_knowledge_base.sql      # 12 entradas de conocimiento IA
│   └── seriagent_saati_exposure.sql      # Datos Saati mesh + exposición
│
├── n8n/
│   ├── SeriAgent_Flow1_BasesDatos.json   # n8n cargador del Vector Store
│   └── SeriAgent_Flow2_Chat.json         # n8n flujo del agente de chat
│
├── knowledge/
│   └── SeriAgent_Knowledge_Base.txt      # Documento de conocimiento RAG
│
├── README.md                             # Versión en inglés
└── README.es.md                          # Este archivo
```

---

## Cómo Funciona el Agente de IA

**Flow 1 — Cargador de Conocimiento:**
1. HTTP Request descarga `SeriAgent_Knowledge_Base.txt` desde GitHub
2. Cohere Embeddings convierte el texto en vectores
3. Simple Vector Store guarda los vectores para búsqueda semántica

**Flow 2 — Agente de Chat:**
1. El usuario envía un mensaje por el chat
2. El Agente de IA busca en el Vector Store el conocimiento relevante
3. Cohere Command R genera una respuesta precisa y contextual
4. Simple Memory mantiene el contexto de la conversación

**Ejemplos de interacciones reales:**
- *"¿Qué malla uso para bolsas tote canvas oscuras?"* → Recomienda malla 110 para base, 150-158 para colores superiores
- *"¿Cuánto cuestan 50 bolsas con 2 colores?"* → Calcula Gs. 2,250,000 automáticamente
- *"La tinta se lava después del primer lavado"* → Diagnostica curado incompleto, da temperaturas exactas

---

## Cómo Ejecutar Este Proyecto

### Opción 1: Oracle APEX (Base de datos + Dashboard)
1. Ir a [apex.oracle.com](https://apex.oracle.com) y solicitar un workspace gratuito
2. En **SQL Workshop > SQL Scripts**, ejecutar `sql/seriagent_full_setup.sql`
3. En **App Builder**, crear una app desde la tabla `FINGERPRINT_ORDERS`

### Opción 2: n8n + Cohere (Agente de IA)
1. Crear una cuenta gratuita en [n8n.io](https://n8n.io)
2. Importar `n8n/SeriAgent_Flow1_BasesDatos.json`
3. Importar `n8n/SeriAgent_Flow2_Chat.json`
4. Agregar tu **API key de Cohere** en ambos flows
5. Ejecutar el Flow 1 para cargar la base de conocimiento
6. Abrir el chat en el Flow 2 y empezar a hacer preguntas

---

## Sobre la Desarrolladora

**Katherine S.** es docente de Lengua y Literatura / ESL en Lumen School, Asunción, Paraguay, con 30 años de experiencia en el aula y un emprendimiento de serigrafía llamado **Fingerprint**, con una sub-marca de impacto social llamada **Heñói**.

Este proyecto conecta su experiencia en tecnología educativa, creación de contenidos y gestión de pequeñas empresas en una solución práctica impulsada por IA.

---

## Contexto del Programa Oracle ONE

- **Programa:** Oracle Next Education (ONE) — Inmersión en IA 2026
- **Enfoque:** Agentes de IA con n8n + Cohere + Oracle APEX
- **Fechas de Inmersión:** 18–22 de mayo de 2026
- **Track:** Full Stack Low-Code con Agentes Inteligentes

---

*Desarrollado con ☕ y tinta en Asunción, Paraguay.*

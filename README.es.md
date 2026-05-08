# SeriAgent by Fingerprint 🖨️

> Un asistente de inteligencia artificial para la gestión de serigrafía, desarrollado para el Programa de Inmersión en IA de Oracle ONE 2026.

---

## ¿Qué es SeriAgent?

SeriAgent es una aplicación web full stack desarrollada con **Oracle APEX** que ayuda a los talleres de serigrafía en Paraguay a gestionar pedidos, resolver problemas técnicos y responder consultas de clientes — todo impulsado por **OCI Generative AI** y **Oracle AI Vector Search**.

Este proyecto fue desarrollado por **Katherine S.** como parte del **Programa de Inmersión en IA de Oracle ONE (mayo 2026)**, con enfoque en **Agentes de IA** aplicados a un negocio real.

**Negocio:** Fingerprint — estudio premium de serigrafía en Asunción, Paraguay.

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
| Panel de Gestión de Pedidos | Oracle APEX + Autonomous DB | ✅ Listo |
| Seguimiento de Clientes y Materiales | Oracle APEX + SQL | ✅ Listo |
| Asistente Técnico con IA | OCI Generative AI (RAG) | 🔧 En desarrollo |
| "Consultá tus Manuales" | Oracle AI Vector Search | 🔧 En desarrollo |
| Soporte Bilingüe (ES/EN) | Globalización en APEX | ✅ Listo |
| Generador de Cotizaciones | PL/SQL + Formularios APEX | 🔧 En desarrollo |

---

## Stack Tecnológico

- **Frontend:** Oracle APEX 24.2 (Low-code, con soporte para Progressive Web App)
- **Base de datos:** Oracle Autonomous Database (Nivel Always Free)
- **Capa de IA:** OCI Generative AI — Llama 3 / Command R+
- **Base de Conocimiento:** Oracle AI Vector Search (pipeline RAG)
- **Nube:** Oracle Cloud Infrastructure (OCI) — Always Free

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
│   ├── 01_create_tables.sql       # Configuración completa del esquema
│   └── 02_sample_data.sql         # Datos de prueba (Murillo Autoservicio, Lumen School)
│
├── apex/
│   └── seriagent_export.sql       # Exportación de la aplicación APEX
│
├── prompts/
│   └── system_prompt.md           # Prompt del sistema para SeriBot AI
│
├── README.md                      # Versión en inglés
└── README.es.md                   # Este archivo
```

---

## Prompt del Sistema (Personalidad de SeriBot)

SeriBot está configurado como un **experto técnico bilingüe (ES/EN)** en serigrafía. Sus características:
- Responde automáticamente en el idioma del usuario
- Proporciona valores técnicos exactos (conteo de mallas, temperaturas de curado, tiempos de exposición)
- Utiliza terminología local de serigrafía paraguaya
- Consulta los manuales técnicos cargados antes de responder (RAG)
- Recuerda al usuario las prácticas de seguridad (ventilación, calor)

Ver prompt completo: [`/prompts/system_prompt.md`](./prompts/system_prompt.md)

---

## Cómo Ejecutar Este Proyecto

### Opción 1: Sandbox de Oracle APEX (sin funciones de IA)
1. Ir a [apex.oracle.com](https://apex.oracle.com) y solicitar un workspace gratuito
2. En **SQL Workshop > SQL Scripts**, ejecutar `sql/01_create_tables.sql` y luego `sql/02_sample_data.sql`
3. En **App Builder**, importar `apex/seriagent_export.sql`

### Opción 2: OCI Always Free (funciones de IA completas)
1. Crear una cuenta gratuita en [oracle.com/cloud/free](https://oracle.com/cloud/free)
2. Aprovisionar una **Autonomous Database**
3. Activar **APEX** y **OCI Generative AI** en tu tenancy
4. Seguir los mismos pasos de importación anteriores
5. En **Workspace Utilities > Generative AI**, configurar las credenciales de OCI

---

## Sobre la Desarrolladora

**Katherine S.** es docente de Lengua y Literatura / ESL en Lumen School, Asunción, Paraguay, con 30 años de experiencia en el aula y un emprendimiento de serigrafía llamado **Fingerprint**, con una sub-marca de impacto social llamada **Heñói**.

Este proyecto conecta su experiencia en tecnología educativa, creación de contenidos y gestión de pequeñas empresas en una solución práctica impulsada por IA.

---

## Contexto del Programa Oracle ONE

- **Programa:** Oracle Next Education (ONE) — Inmersión en IA 2026
- **Enfoque:** Agentes de IA con Oracle APEX + OCI Generative AI
- **Fechas de Inmersión:** 18–22 de mayo de 2026
- **Track:** Full Stack Low-Code con Agentes Inteligentes

---

*Desarrollado con ☕ y tinta en Asunción, Paraguay.*

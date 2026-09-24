# Project Brief: Multimax CRM (Operativo Pro)

This document provides a comprehensive overview of the Multimax CRM project, designed to serve as a foundational brief for an AI-powered agent (like opencode) to understand, document, and represent the project in a GitHub portfolio repository.

---

## 1. Executive Summary
**Multimax CRM** is a robust, mobile-first operational CRM tailored for small and medium-sized cleaning supply companies (PyMEs) in Argentina. It centralizes client management, differentiated pricing structures, automated WhatsApp communications, and AI-driven catalog processing into a streamlined, high-performance platform.

## 2. Technical Stack
### Frontend
- **Framework:** React + Vite + TypeScript.
- **Styling:** Tailwind CSS (customized "Serene Air" design system).
- **Features:** PWA (Progressive Web App) for mobile-first operational usage.
- **Icons:** Lucide React.
- **State/Navigation:** Custom hooks and routing for a seamless single-page experience.

### Backend
- **Runtime:** Node.js + Express + TypeScript.
- **ORM:** Prisma ORM.
- **Queue System:** BullMQ + Redis (for asynchronous messaging tasks).
- **Architecture:** Modular controllers and services.

### Database & Infrastructure
- **Development:** SQLite.
- **Production:** PostgreSQL (Dockerized).
- **Orchestration:** Docker Compose (Express, Postgres, Redis).
- **Process Management:** Custom `start.sh` for reliable local development startup with port detection.

## 3. Core Modules & Functionality
### CRM Core
- **Client Directory:** Multi-view (Table/Grid) management of clients with delivery addresses, payment conditions, and account balances.
- **Differentiated Pricing:** Automatic price calculation based on client segments (e.g., Wholesaler, Retailer, Distributor) via margin multipliers or fixed prices.
- **Sales Lifecycle:** Tracking from "Presupuesto" (Quote) to "Entregado" (Delivered) and "Cobrado" (Paid), with automatic commission calculations.

### WhatsApp Automation
- **Inbound Bot (FSM):** A Finite State Machine that qualifies new leads automatically via WhatsApp (Greeting -> Business Type -> Zone -> Price List delivery).
- **Mass Broadcast:** Asynchronous message dispatching with rate-limiting and jitter to prevent WhatsApp API bans.
- **Interaction Logging:** Full history of bot-client conversations stored in the database.

### Intelligent Catalog (AI)
- **DeepSeek API Integration:** Automated extraction of structured product data (names, codes, prices, presentations) from uploaded PDF/Image catalogs.
- **Dynamic Updates:** Preview and bulk-update system price lists based on AI-parsed documents.

### Operational Agenda
- **Interactive Calendar:** A Google Calendar-style weekly/daily grid for managing deliveries, meetings, and sales tasks.
- **Relational Linking:** Mandatory linking of deliveries to specific orders and clients.
- **Visual Hierarchy:** Color-coded categorization (Deliveries, Tasks, Meetings, Reminders).

### Operational Dashboard
- **Executive Metrics:** Real-time visibility into monthly billing, accrued commissions, and pending collections.
- **Churn Detection:** Automatic alerting for clients who haven't placed orders within a configurable threshold (e.g., 30 days).

## 4. Design System (Serene Air)
- **Aesthetic:** Breathable, ultra-clean, and "serene" B2B workflow.
- **Colors:** Deep Navy base (`#0F172A`), Radiant Blue primary (`#2563EB`), Emerald secondary (`#10B981`), and Amber warnings.
- **Typography:** Plus Jakarta Sans for high legibility in data-dense views.
- **Layout:** Sidebar-driven desktop view and persistent bottom-navigation for mobile.

## 5. Security & Scaling
- **Authentication:** JWT-based auth with Role-Based Access Control (Admin, Seller, Coordinator).
- **Scaling Path:** Migration from SQLite to containerized PostgreSQL for high concurrency.
- **Process Resilience:** Shell scripts with signal traps for clean shutdowns and robust service orchestration.

---

*This document was auto-generated to represent the architectural and functional depth of the Multimax CRM project.*

---

## Contexto profesional

**Rol en el portfolio:** proyecto personal full-stack que aplica el patrón de un producto B2B operativo de punta a punta, sobre una base backend sólida.

**Conexión con mi trayectoria:** el backend Node.js/Express con PostgreSQL dockerizado y la separación entre la operación interactiva y la mensajería masiva encolada (BullMQ + Redis) reflejan el trabajo con APIs y servicios de alta demanda que realizo en sistemas financieros críticos. La autenticación con JWT y RBAC replica el control de acceso que aplico en entornos productivos, y la extracción de catálogo con DeepSeek conecta directamente con mi línea de AI Engineering (integración de LLM sobre base backend).

**Qué demuestra:** capacidad de llevar un producto completo —modelo de datos, API, interfaz, colas asíncronas e infraestructura— con decisiones de arquitectura justificadas y no solo funcionalidad.

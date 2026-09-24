# OdontoSoft — Plataforma Integral para Clínicas Odontológicas

> **Propósito de este documento**: Este archivo contiene el contexto técnico, arquitectónico y funcional completo de **OdontoSoft** diseñado para que una IA (`opencode`) o un desarrollador pueda comprender en profundidad el proyecto y generar un repositorio de GitHub de portfolio de nivel senior (incluyendo estructura, documentación de arquitectura, decisiones técnicas y manuales de desarrollo).

---

## 1. Visión General del Proyecto

**OdontoSoft** es una solución de software como servicio (SaaS) web-first diseñada para la gestión clínica, operativa y administrativa de clínicas odontológicas de tamaño pequeño y mediano. 

Resuelve problemas críticos de la operación dental cotidiana:
- **Agenda Multirrecurso con Drag & Drop**: Gestión simultánea de sillones y profesionales, evitando solapamientos y facilitando la creación y reprogramación de turnos.
- **Ficha Clínica Completa y Segura (RBAC)**: Separación estricta entre la información administrativa, financiera y clínica, con control de acceso por roles (Administrador, Odontólogo, Recepción, Asistente).
- **Odontograma FDI Interactivo**: Registro gráfico y textual de tratamientos, piezas y caras dentales bajo la norma FDI.
- **Trazabilidad y Auditoría de Turnos**: Máquina de estados robusta para el ciclo de vida del turno (`SIN_CONFIRMAR`, `CONFIRMADO`, `EN_SALA`, `ATENDIDO`, `AUSENTE`, `CANCELADO`, `REPROGRAMADO`) con historial inmutable de cambios (`historialEstados`).

---

## 2. Stack Tecnológico

### Frontend
- **Framework**: React 18 con TypeScript (`vite` como bundler).
- **Enrutamiento**: `react-router-dom` v6 (rutas anidadas y lazy loading de módulos).
- **Estado Global**: Zustand (stores modulares desacoplados: `agenda`, `pacientes`, `odontograma`, `tareas`, `sesion`, `catalogo`).
- **Estilos y UI**: Tailwind CSS, Radix UI (primitivos accesibles para modales, popovers y dropdowns), Lucide React (iconografía).
- **Interacción Avanzada**: `@dnd-kit/core` y `@dnd-kit/utilities` para manipulación táctil y de mouse en la agenda.

### Backend y Persistencia
- **Runtime**: Node.js con Express 5 y TypeScript (`tsx` para ejecución y desarrollo).
- **Capa de Datos**: PostgreSQL utilizando **Drizzle ORM** para tipado estricto y migraciones seguras.
- **Capa de Repositorios**: Abstracción frontend mediante repositorio dual (`mockRepo` para desarrollo local en memoria / `httpRepo` listo para conectar con API REST).

### Testing y Calidad
- **Pruebas Unitarias/Integración**: Vitest para validación de lógica de negocio, máquinas de estado de turnos y motores de conflicto.
- **Linting y Tipado**: TypeScript estricto (`tsc --noEmit`) y ESLint.

---

## 3. Módulos y Arquitectura Funcional

### A. Agenda y Calendario (`src/modules/agenda/`)
- **Vistas**: Día, Semana y Mes.
- **Interacción de Creación**: Selección vertical por arrastre (*drag-and-drop*) en celdas horarias libres. Un click simple crea un bloque de 30 minutos; el arrastre calcula dinámicamente la hora de inicio y fin.
- **Bloqueos y Ausencias**: Distinción clara entre *Bloqueos de Agenda* (afectan sillones o profesionales específicos) y *Ausencias de Personal* (franco, licencia).
- **Validación de Conflictos**: Comprobación algorítmica de solapamiento horario previa al almacenamiento.

### B. Pacientes y Ficha Clínica (`src/modules/pacientes/`)
- **Directorio de Pacientes**: Búsqueda rápida, filtros por cobertura y estado de cuenta.
- **Ficha Modular por Pestañas**:
  1. *Resumen*: Alertas médicas destacadas, próximo turno y saldo pendiente.
  2. *Datos Personales*: Información de contacto y cobertura (obra social y número de afiliado).
  3. *Turnos*: Listado separado en próximos e historial.
  4. *Visitas / Evoluciones*: Línea de tiempo cronológica. Prescripción restringida únicamente al rol `ODONTOLOGO` o `ADMIN`.
  5. *Odontograma*: Grilla dental interactiva con restricciones clínicas por rol.
  6. *Cuenta Corriente*: Libro de movimientos y saldo pendiente de caja por paciente.

### C. Odontograma Interactivo (`src/modules/odontograma/`)
- Basado en el sistema **FDI (Federación Dental Internacional)**.
- Permite seleccionar piezas dentales (permanentes y temporales) y aplicar marcas específicas por cara (oclusal, mesial, distal, vestibular, lingual/palatina) o tratamientos globales sobre la pieza.

### D. Control de Acceso por Roles (RBAC)
Definido en `src/types/index.ts`:
- **Roles**: `ADMIN`, `ODONTOLOGO`, `RECEPCION`, `ASISTENTE`.
- **Reglas clave**: 
  - Solo `ADMIN` y `RECEPCION` acceden a Finanzas y Equipo.
  - Solo `ODONTOLOGO` y `ADMIN` pueden prescribir en evoluciones clínicas y editar el odontograma.
  - Selector dinámico de rol en la barra superior (`TopBar`) para pruebas en tiempo real sin recargar la sesión.

---

## 4. Estructura de Directorios del Repositorio

```text
odontosoft/
├── server/               # Backend Express + Drizzle ORM (Schema, migraciones, seed)
│   ├── api.ts            # Endpoints REST principales
│   └── db/               # Configuración de PostgreSQL, esquemas y seeders
├── src/                  # Aplicación Frontend React
│   ├── components/       # Componentes UI reutilizables y layout base (TopBar, Nav)
│   ├── data/             # Repositorios (httpRepo / mockRepo)
│   ├── modules/          # Módulos de negocio (agenda, pacientes, finanzas, tareas, odontograma)
│   ├── store/            # Stores Zustand (estado global reactivo)
│   ├── types/            # Contratos de tipos compartidos (RolUsuario, Turno, Paciente, etc.)
│   └── App.tsx           # Shell principal y enrutamiento con React Router
├── tests/                # Suites de pruebas con Vitest (turnos, backend, tareas)
├── docs/                 # Documentación de dominio, decisiones de arquitectura y métricas
└── openspec/             # Especificaciones técnicas estructuradas por cambios
```

---

## 5. Instrucciones para la IA en el Nuevo Repositorio de Portfolio

Si deseas que una IA genere este portfolio en un repositorio nuevo a partir de este documento, pídele lo siguiente:

> *"Crea una aplicación web moderna tipo portfolio basada en la especificación de OdontoSoft: un sistema de gestión para clínicas odontológicas con una interfaz impecable en React, Tailwind CSS y TypeScript. Incluye simulación interactiva de una agenda con drag-and-drop, ficha de pacientes con pestañas, selector de roles en tiempo real y un odontograma FDI interactivo. El diseño debe ser limpio, profesional, con tonos clínicos (emerald/teal/slate), siguiendo una arquitectura modular por componentes."*

---

## Contexto profesional

**Rol en el portfolio:** SaaS web-first con backend Express + Drizzle/PostgreSQL y frontend React + TypeScript, centrado en dominio clínico.

**Conexión con mi trayectoria:** la máquina de estados del turno con historial inmutable y la separación estricta de RBAC entre lo clínico y lo administrativo replican el rigor transaccional y de control de acceso que ejerzo en sistemas financieros (estándares ACID, procesos batch, JWT/OAuth 2.0). La abstracción de repositorio (`mockRepo`/`httpRepo`) y el testing con Vitest reflejan las prácticas de Clean Code y testing que aplico en producción.

**Qué demuestra:** diseño de dominio con invariantes y trazabilidad —no solo CRUD— y un frontend complejo construido sobre una base backend fuerte.

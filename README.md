# Cinco Sentidos - Asistente IA de Cosmetología

Proyecto integrador del curso **AI Automation Avanzado** (Coderhouse 2026).

**Alumna:** María Laura Menafra

---

## Sobre el proyecto

**Cinco Sentidos** es un centro de cosmetología para el cual se desarrolló un sistema de atención automatizada usando **n8n** como plataforma de automatización e inteligencia artificial.

El asistente recibe consultas de clientes por múltiples canales (Gmail y Telegram), las clasifica automáticamente mediante un modelo de lenguaje (LLM) y las deriva a flujos especializados según el tipo de consulta: productos, tratamientos, turnos o consultas generales.

## Arquitectura general

```
Cliente (Gmail / Telegram)
    ↓
Manager Multicanal (workflow principal)
    ↓
Clasificador LLM (Groq)
    ↓
┌─────────────┬──────────────────┬──────────────┐
│  Productos  │  Tratamientos    │  Turnos/Otro │
│  (Worker)   │  (Worker)        │  (Directo)   │
└─────────────┴──────────────────┴──────────────┘
    ↓
Respuesta al cliente por canal original
    ↓
Memoria persistente (Google Sheets) + Supervisión (Slack)
```

## Tecnologías utilizadas

- **n8n Cloud** — Plataforma de automatización de workflows
- **Groq** — Modelo LLM para clasificación de consultas
- **Gmail API** (OAuth2) — Recepción de correos y borradores HITL
- **Telegram Bot API** — Canal de atención por chat
- **Google Sheets** (OAuth2) — Memoria persistente de sesiones
- **Slack** (OAuth2) — Notificaciones de supervisión al equipo
- **Salesforce** (OAuth2) — Integración CRM

## Entregas por módulo

| Carpeta | Módulo | Contenido |
|---------|--------|-----------|
| `TP1/` | Módulo 1 | Primer flujo básico del asistente |
| `tp2/` | Módulo 2 | Workflow con sub-workflows de catálogo y tratamientos |
| `TP3/` | Módulo 3 | Manager con documentación y pruebas de flujo completo |
| `TP4/` | Módulo 4 | Manager Multicanal final con credenciales seguras, manejo de errores y HITL |
| `TP6/` | Módulo 6 | Iteración avanzada del flujo |

## Características principales

- **Multicanal:** Atiende consultas por Gmail y Telegram desde un único flujo
- **Clasificación inteligente:** LLM categoriza la intención del cliente (producto, tratamiento, turno, otro)
- **Patrón Manager-Worker:** Workflow principal delega a sub-workflows especializados
- **Human-in-the-Loop (HITL):** Crea borradores en Gmail para revisión humana antes de enviar
- **Memoria persistente:** Guarda historial de conversaciones en Google Sheets por Session_ID
- **Supervisión:** Notifica al equipo en Slack con resumen de cada consulta procesada
- **Manejo de errores:** Validación de JSON, fallbacks, control de duplicados y `onError` en nodos críticos

---

*Proyecto desarrollado como parte del curso AI Automation Avanzado — Coderhouse 2026*

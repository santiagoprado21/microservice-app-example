# Estrategia de Branching para Desarrolladores

## 🧩 Tipo de Estrategia

**Trunk-Based Development (TBD)**

Los desarrolladores siguen una estrategia basada en Trunk-Based Development, enfocada en integración continua, ramas de corta duración y despliegue rápido.

---

## 🌳 Estructura de Ramas

- Rama principal: `master` (rama de producción)
- Ramas de desarrollo: `feature/*` creadas desde `master`
- Cada microservicio puede tener sus propias ramas `feature/*`
- No hay ramas `develop`, `release`, `hotfix` ni `support`

---

## 🔄 Flujo de Desarrollo

1. Se crea una rama `feature/nombre-de-la-caracteristica` desde `master`
2. Se desarrolla la funcionalidad
3. Se abre un Pull Request hacia `master`
4. Se realiza revisión de código
5. Se ejecutan pruebas automatizadas y validaciones de CI
6. Si todo pasa, se fusiona a `master`

---

## ⚙️ Integración Continua

- Cada microservicio tiene su propio pipeline de CI:
  - `auth-api-ci.yml`
  - `frontend-ci.yml`
  - `log-message-processor-ci.yml`
  - `todos-api-ci.yml`
  - `users-api-ci.yml`
- Las pruebas y validaciones se ejecutan en cada push o PR

---

## 🚀 Despliegue

- Despliegue automático se activa cuando:
  - Los cambios se fusionan en `master`
  - Todas las pruebas CI pasan exitosamente
  - El pipeline central de CD (`cd.yml`) se ejecuta correctamente

---

## ✅ Características de TBD que se cumplen

- Integración frecuente a `master`
- Ramas de corta duración
- Sin ramas paralelas de mantenimiento
- Automatización de pruebas y despliegues
- Flujo simple, directo y eficiente

---

## 🎯 ¿Por qué es adecuada esta estrategia para desarrolladores?

- Es un **proyecto de microservicios**
- El equipo es **pequeño**
- Se requiere **entrega continua**
- Hay **automatización de pruebas**
- Se evita la complejidad de flujos como Git Flow

# Estrategia de Branching para Operaciones

## 🧩 Tipo de Estrategia

**Trunk-Based Development (TBD)**

Esta estrategia también se aplica al área de operaciones en este proyecto, ya que todo el proceso de despliegue y automatización sigue el mismo enfoque que el desarrollo: integración continua en una única rama principal (`master`), sin ramas de soporte o mantenimiento.

---

## 🌳 Estructura de Ramas

- Única rama principal: `master`
- Ramas temporales y de corta duración para `feature/*`
- **No existen ramas de:**
  - Mantenimiento (`maintenance`)
  - Soporte (`support`)
  - Releases (`release/*`)
  - Hotfixes (`hotfix/*`)

---

## ✅ Características de TBD presentes en operaciones

- **Integración frecuente a `master`**
- Ramas de vida corta enfocadas en una sola funcionalidad o fix
- **Despliegue continuo** (CD)
- Automatización con pipelines desde `master`
- No hay ramas paralelas de mantenimiento

---

## 🧾 Evidencia en el Código

- Archivo `cd.yml` define despliegue automático desde `master`
- No se observan ramas de mantenimiento, soporte ni releases
- Todo el código de infraestructura (CI/CD) se gestiona desde `master`
- Las correcciones también se realizan desde ramas `feature/*`

---

## 🛠️ Proceso de Operaciones

1. Se crean ramas de `feature/*` si se requiere modificar infraestructura o despliegue.
2. Cambios se integran a `master` mediante Pull Requests.
3. Si todas las pruebas automatizadas pasan, el despliegue se ejecuta automáticamente.
4. No hay flujos separados para infraestructura o operaciones: todo vive en el mismo trunk (`master`).

---

## 🎯 ¿Por qué es adecuada esta estrategia para operaciones?

- Es un **proyecto de microservicios**
- El equipo es **pequeño**, por lo que se evita complejidad innecesaria
- Se requieren **despliegues frecuentes** y rápidos
- Las pruebas están **automatizadas**
- No se necesitan ramas de soporte ni flujos separados de mantenimiento

---


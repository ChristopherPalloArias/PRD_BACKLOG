<div align="center">
  
# 🚀 TICKETING_MVP_MASTER_HUB

### Taller Semana 7: Expectativa vs. Realidad - Ejecución Ágil, MVP y Estrategia de Pruebas

**Equipo:** Christopher Ismael Pallo Arias (QA) / DEV  
**Proyecto:** Construcción del Ticketing MVP Real y Certificación Integral de Calidad  
**Objetivo:** Vivir "el choque con la realidad". Pasar del diseño utópico del Taller 6 a la construcción e integración de las piezas críticas para entregar un Producto Mínimo Viable funcional. Consolidar aquí la documentación rectora estratégica (Plan de Pruebas y Matrices) y enlazar todo el ecosistema de automatización.

<br />

### 🛠️ Ecosistema Tecnológico Distribuido

**Microservicios | API BDD | Performance | Functional UI/API**
<br />
<img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java" />
<img src="https://img.shields.io/badge/Spring_Boot-F2F4F9?style=for-the-badge&logo=spring-boot" alt="Spring" />
<img src="https://img.shields.io/badge/Karate-1.5.0-black?style=for-the-badge&logo=karate" alt="Karate DSL" />
<img src="https://img.shields.io/badge/k6-1.7.0-7D64FF?style=for-the-badge&logo=k6&logoColor=white" alt="k6" />
<img src="https://img.shields.io/badge/Serenity_BDD-4E9A06?style=for-the-badge" alt="Serenity" />
<img src="https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL" />

</div>

---

## 📌 Panel Documental de Estrategia (Fase 3 y 5)

> ⚠️ **ATENCIÓN EVALUADOR:** Este repositorio funciona como el **Control Central (Hub)**. Aquí residen exclusivamente los artefactos estratégicos y de planificación ágil exigidos por la rúbrica del Taller 7, que orquestan las pruebas de todo el proyecto.

- 📄 **Plan de Pruebas Oficial:** [`TEST_PLAN.md`](./TEST_PLAN.md) *(Documentación estricta de alcance, estrategia, matrices de riesgo y cronograma QA).*
- 📋 **Matriz de Casos de Prueba:** [`TEST_CASES.md`](./TEST_CASES.md) *(Mapeo detallado de las 7 Historias de Usuario, precondiciones y resultados de los 29 escenarios).*
- 🔍 **Análisis Retrospectivo:** [`REALITY_CHECK.md`](./REALITY_CHECK.md) *(Documento de Cierre: Expectativa vs. Tiempo Real invertido por el equipo).*
- 🧠 **Cimientos de Producto:** Las carpetas y archivos legados de este repositorio (`PRD.md`, `USER_STORIES.md`, etc.) brindan trazabilidad a los requerimientos de negocio devenidos en este MVP.

---

## 🌌 Ecosistema de Repositorios (Código y Automatización)

Para cumplir con la separación de responsabilidades, aislar el rendimiento y mantener la limpieza de la integración continua, el proyecto está fragmentado en **4 repositorios satélite fundamentales**. 

Cada repositorio cuenta con un nivel de cumplimiento extremo, README propio con explicaciones de sus retos técnicos y despliegues automáticos a GitHub Pages.

| Perfil / Dominio | Repositorio Oficial | Resultados en Vivo |
|---|---|---|
| 🏗️ **Backend & Orquestación** | [🔗 **TICKETING_SEM7**](https://github.com/ChristopherPalloArias/TICKETING_SEM7) | *Microservicios Base (Docker Compose)* |
| 🥋 **Certificación Funcional** | [🔗 **TICKETING_SEM7_KARATE**](https://github.com/ChristopherPalloArias/TICKETING_SEM7_KARATE) | [🌐 Dashboard Karate](https://christopherpalloarias.github.io/TICKETING_SEM7_KARATE/) |
| 🚀 **Pruebas de Carga (SLA)** | [🔗 **TICKETING_SEM7_K6**](https://github.com/ChristopherPalloArias/TICKETING_SEM7_K6) | [🌐 Informe k6](https://christopherpalloarias.github.io/TICKETING_SEM7_K6/) |
| 🥒 **Pruebas BDD (Funcional)** | [🔗 **TICKETING_SEM7_SERENITY**](https://github.com/ChristopherPalloArias/TICKETING_SEM7_SERENITY) | *Suites de Serenity BDD* |

---

## 🎯 Contexto del Reto: El Choque con la Realidad

En el Taller 6 (fase de diseño en este mismo backlog) diseñamos el plano de un ecosistema perfecto. En el **Taller 7**, la misión fue priorizar basándonos en el riesgo de negocio: construir un núcleo capaz de soportar la venta real, evitando sobreventas y bloqueos de entradas por carritos abandonados.

### Dinámica de Trabajo y Fases
1. **Fase 1 (Alineación):** Dejamos de lado historias cosméticas o pasarelas completas y abrazamos la selección de 7 HUs de núcleo para un MVP realista en torno a la disponibilidad concurrente.
2. **Fase 2 (Ejecución):** El DEV implementó a contrarreloj en micro-sprints de 2 días los microservicios transaccionales. Aquí nació la primera desviación técnica debido a orquestaciones asíncronas imprevistas.
3. **Fase 3 (Estrategia QA):** Mientras se construía, se cimentó el Plan de Calidad (ver archivos de este repo). No fue probar por probar, sino probar lo que sostiene el negocio.
4. **Fase 4 (Reto Karate Automatizado):** Se generaron 29 casos de prueba robustos mapeados 1 a 1 a las Historias de Usuario para validar contratos (Schema Match), reglas temporales y concurrencia.
5. **Fase 5 (Análisis Retrospectivo):** Se contrastan los Story Points estimados contra los obstáculos técnicos afrontados, sintetizado en el documento de check-in de realidad.

---

## 🧭 ¿Cómo Auditar Este Proyecto?

Si estás evaluando la entrega, te sugerimos este orden de revisión:
1. **Lee la Estrategia:** Abre primero el [`TEST_PLAN.md`](./TEST_PLAN.md) en este repositorio para comprender cómo, qué y por qué se automatizó lo que se automatizó.
2. **Revisa la Ejecución de Pruebas:** Dirígete a los Dashboards vivos de [Karate](https://christopherpalloarias.github.io/TICKETING_SEM7_KARATE/) y [k6](https://christopherpalloarias.github.io/TICKETING_SEM7_K6/) usando la tabla superior.
3. **Reflexiona con el Equipo:** Finaliza revisando el [`REALITY_CHECK.md`](./REALITY_CHECK.md) para constatar nuestra madurez técnica ante los imprevistos de un sprint ágil real.
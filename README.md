<div align="center">
  
# 🚀 TICKETING_MVP_MASTER_HUB

### Taller Semana 7: Expectativa vs. Realidad - Ejecución Ágil, MVP y Estrategia de Pruebas

**Equipo del Proyecto:**  
Christopher Ismael Pallo Arias — **QA**  
Luis Alfredo Pinzón Quintero — **DEV**

**Proyecto:** Construcción del Ticketing MVP Real y Certificación Integral de Calidad  
**Objetivo:** Vivir "el choque con la realidad". Pasar del diseño utópico del Taller 6 a la construcción e integración de las piezas críticas para entregar un Producto Mínimo Viable funcional. Consolidar aquí la documentación rectora estratégica (PRD, Plan de Pruebas y Matrices) y enlazar todo este ecosistema interconectado.

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

## 🎭 Sobre el Producto (Contexto de Negocio)

**Sistema de Venta de Entradas para Obras de Teatro**  
El sistema resuelve el problema histórico del inventario bloqueado: cuando un comprador intenta adquirir una entrada pero no completa el pago, el sistema tradicional congela la venta. 

Nuestro MVP orquesta un **temporizador ágil de 10 minutos** respaldado por jobs de sincronización y validaciones optimistas de inventario. Si el pago falla o el tiempo expira, las entradas se liberan instantánea y automáticamente. Para el espectador significa transparencia; para el organizador, maximización de ingresos y cero sobreventas.

**Características Núcleo Construidas en este MVP:**
- Configuración de aforos estrictos y validación de topes por sala.
- Estructuración dinámica de categorías (Tiers): *VIP, General, y Early Bird* (basado en tiempo).
- Reserva con cuenta regresiva.
- Simulador de transacciones (Éxito / Fallo de tarjetas).
- Liberación asíncrona de entradas abandonadas.

### 📚 Glosario Transversal
*   **Tier:** Categorías de las entradas disponibles para un evento.
*   **Early Bird:** Categoría con precio especial disponible solo durante una ventana de tiempo definida.
*   **Reserva:** Bloqueo temporal de una entrada mientras el comprador completa el pago.
*   **Timeout & Timer:** Vencimiento automático de la reserva.
*   **Scheduler & Job de respaldo:** Procesos silentes que barren reservas abandonadas garantizando disponibilidad perpetua.

---

## 🌌 Ecosistema de Repositorios (Código y Automatización)

Para cumplir con la separación de responsabilidades y aislar la infraestructura y testing, el proyecto está fragmentado en **4 repositorios satélite fundamentales**. 

| Perfil / Dominio | Repositorio Oficial | Resultados en Vivo |
|---|---|---|
| 🏗️ **Backend & Aplicación** | [🔗 **TICKETING_SEM7**](https://github.com/ChristopherPalloArias/TICKETING_SEM7) | *Microservicios Base (Toda la app)* |
| 🥋 **Certificación Funcional** | [🔗 **TICKETING_SEM7_KARATE**](https://github.com/ChristopherPalloArias/TICKETING_SEM7_KARATE) | [🌐 Dashboard Karate](https://christopherpalloarias.github.io/TICKETING_SEM7_KARATE/) |
| 🚀 **Pruebas de Carga (SLA)** | [🔗 **TICKETING_SEM7_K6**](https://github.com/ChristopherPalloArias/TICKETING_SEM7_K6) | [🌐 Informe k6](https://christopherpalloarias.github.io/TICKETING_SEM7_K6/) |
| 🥒 **Pruebas BDD (Funcional)** | [🔗 **TICKETING_SEM7_SERENITY**](https://github.com/ChristopherPalloArias/TICKETING_SEM7_SERENITY) | *Suites de Serenity BDD* |

---

## 📌 Documentación de Producto y Estrategia QA

### Fase Taller 6: Concepción del Producto (Diseño)
Aquí diagramamos la base de nuestro negocio, los requerimientos y las historias.
- 📐 **Historia y Flujos:** [Revisar tablero Story Map interactivo en FigJam](https://www.figma.com/figjam) (Flujos MVP, Planning Poker, Actividades).
- 🏗️ **Documento PRD:** [`PRD.md`](./PRD.md)
- 👤 **Historias de Usuario:** [`USER_STORIES.md`](./USER_STORIES.md)
- ☑️ **Subtareas DEV:** [`SUBTASKS.md`](./SUBTASKS.md)

### Fase Taller 7: Estrategia de Pruebas (El Choque con la Realidad)
Aquí consolidamos la estrategia de validación exigida por rúbrica para certificar los micro-sprints del DEV. Todo escenario construido en K6, Karate o Serenity obedece a las matrices de este nivel documental.
- 📊 **Gestión Ágil:** [Tablero GitHub Projects](https://github.com/users/ChristopherPalloArias/projects/2) *(Seguimiento de las Historias de Usuario desarrolladas y subtareas).*
- 📄 **Plan de Pruebas Oficial:** [`TEST_PLAN.md`](./TEST_PLAN.md) *(Validación estricta de alcance, estrategia formal, ambientes y aserciones de la Fase 3).*
- 📋 **Matriz de Casos de Prueba:** [`TEST_CASES.md`](./TEST_CASES.md) *(Mapeo detallado de las 7 Historias de Usuario desarrolladas y sus 29 casos operacionales automatizados).*
- 🔍 **Análisis Retrospectivo:** [`REALITY_CHECK.md`](./REALITY_CHECK.md) *(Documento de Cierre conjunto DEV+QA, análisis de desvíos y retrospectiva).*

---

## 🧭 ¿Cómo Auditar Este Proyecto Completo? (Taller 7)

Si estás evaluando el cumplimiento de todos los hitos del taller para la calificación compartida (QA 50% / DEV 50%), te sugerimos este estándar de revisión:
1. **Entender el Contexto de Riesgo:** Abre aquí mismo el [`TEST_PLAN.md`](./TEST_PLAN.md) para verificar cómo priorizamos agresivamente las pruebas funcionales.
2. **Revisión de Flujos Funcionales:** Ingresa al Dashboard vivo de **[Karate](https://christopherpalloarias.github.io/TICKETING_SEM7_KARATE/)** que certifica en BDD que no permitimos sobreventas.
3. **Revisión de SLA y Rendimiento:** Verifica la carga paramétrica asíncrona inyectada contra el servidor en el reporte público de **[K6](https://christopherpalloarias.github.io/TICKETING_SEM7_K6/)**.
4. **Cierre de Ciclo:** Evalúa las lecciones de micro-sprint leyendo las respuestas del equipo en nuestro [`REALITY_CHECK.md`](./REALITY_CHECK.md).
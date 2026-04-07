# TEST_PLAN.md
## Sistema de Venta de Entradas — Ticketing MVP

## 1. Identificación del Plan

| Campo | Detalle |
|---|---|
| **Proyecto** | Sistema de Venta de Entradas para Obras de Teatro |
| **Sistema bajo prueba** | `ms-events`, `ms-ticketing`, `ms-notifications` |
| **Versión** | MVP v1.0 |
| **Fecha** | 26/03/2026 |
| **Equipo** | Christopher Ismael Pallo Arias (QA) — Luis Alfredo Pinzón Quintero (DEV) |

---

## 2. Contexto

El sistema a probar es una plataforma de ticketing para obras de teatro orientada a resolver un problema de negocio concreto: evitar que las entradas queden bloqueadas cuando un comprador no finaliza el pago. El MVP busca asegurar disponibilidad real del inventario, permitiendo al administrador crear eventos y configurar tiers, y al comprador consultar disponibilidad, reservar por 10 minutos, pagar con simulación y visualizar su ticket confirmado.

El valor del MVP depende de que el inventario se mantenga consistente, de que no exista sobreventa y de que la entrada se libere automáticamente cuando el pago falla o la reserva expira. El objetivo de este ciclo no es cubrir todo el backlog, sino validar el núcleo funcional que realmente entrega valor al negocio dentro de micro-sprints de 2 días.

---

## 3. Alcance de las Pruebas

### 3.1 Historias incluidas en este ciclo MVP

| Historia | Nombre | SP |
|---|---|---:|
| HU-01 | Creación de evento de obra de teatro | 5 |
| HU-02 | Configuración de tiers y precios por evento | 5 |
| HU-03 | Visualización de eventos y disponibilidad | 3 |
| HU-04 | Reserva y compra de entrada con pago simulado | 8 |
| HU-05 | Liberación automática por fallo de pago o expiración | 8 |
| HU-06 | Notificaciones al comprador | 3 |
| HU-07 | Visualización de ticket confirmado | 2 |

**Total en alcance:** 34 SP

### 3.2 Cobertura funcional incluida

Este plan cubre el núcleo del negocio definido en el PRD:

- Creación de eventos con aforo configurable.
- Validación de aforo contra la capacidad máxima de la sala.
- Configuración de tiers **VIP, General y Early Bird**.
- Validación de cupos y precios por tier.
- Vigencia temporal del tier **Early Bird**.
- Visualización de eventos disponibles y disponibilidad vigente por tier.
- Flujo de reserva con vigencia máxima de **10 minutos**.
- Pago simulado con resultado exitoso o fallido.
- Liberación automática de entradas por expiración o rechazo de pago.
- Notificaciones internas al comprador.
- Visualización del ticket confirmado únicamente tras compra exitosa.

### 3.3 Fuera de alcance en este ciclo

- Registro de administrador y comprador.
- Inicio de sesión y autenticación real con JWT.
- Pasarela de pago real.
- Cancelaciones y reembolsos.
- Reportes y métricas de ventas.
- Integración con correo o mensajería real.
- App móvil nativa.
- Soporte multilenguaje.
- Selección avanzada de asientos numerados.
- Promociones distintas a **Early Bird**.
- Funcionalidades fuera del núcleo del MVP.

**Nota de alcance:** el sistema se valida en un **contexto controlado**, con usuarios previamente habilitados y con rol administrado por headers o mecanismos equivalentes del entorno de prueba.

---

## 4. Estrategia de Pruebas

La estrategia se enfoca en validar primero las funcionalidades críticas del MVP y en documentar formalmente la cobertura del sprint.

### 4.1 Tipos de prueba

| Tipo de prueba | Herramienta | Propósito |
|---|---|---|
| **Funcional** | SerenityBDD + Cucumber | Automatizar criterios de aceptación en Gherkin por cada HU del MVP |
| **API** | Karate DSL | Validar contratos, códigos HTTP, estructura JSON y reglas de negocio de los servicios |
| **Rendimiento** | k6 | Validar comportamiento bajo carga sobre los flujos críticos del backend. Umbrales definidos: `GET /api/v1/events` → p95 < 400 ms, mínimo 80 TPS · `POST /api/v1/reservations` → p95 < 600 ms, mínimo 30 TPS. Estas pruebas no sustituyen la cobertura funcional de Karate; se enfocan exclusivamente en latencia, throughput, tasa de error y estabilidad bajo carga |
| **Validación de datos** | SQL directo sobre PostgreSQL + mecanismos de soporte del entorno de prueba | Verificar consistencia de inventario, estados de reserva y tickets como capa de evidencia adicional a la respuesta HTTP y a los flujos automatizados. |
| **Manual / exploratoria** | Apoyo QA | Revisar temporizador, mensajes, disponibilidad visible, estados y bordes funcionales |

### 4.2 Enfoque de cobertura

- Se priorizan las historias que sostienen el valor del negocio: disponibilidad real, reserva temporal, liberación automática, notificaciones y ticket confirmado.
- Cada HU se cubre con sus criterios de aceptación y con los casos de prueba ya definidos en GitHub Projects.
- La trazabilidad documental se mantendrá entre:
  - `PRD.md`
  - `USER_STORIES.md`
  - `SUBTASKS.md`
  - `TEST_CASES.md`
  - subtareas de casos de prueba en GitHub Projects

### 4.2.1 Criterio de priorización basado en riesgo

Dado que las pruebas exhaustivas no son viables, la estrategia de este ciclo adopta un enfoque de priorización basado en riesgo. En consecuencia, el esfuerzo de QA se concentra primero en las historias que sostienen el valor central del MVP y que representan mayor impacto para el negocio: disponibilidad real del inventario, reserva temporal, liberación automática de entradas, integridad de la compra y prevención de sobreventa.

Este criterio permite enfocar la cobertura en los flujos más sensibles del producto sin ampliar innecesariamente el alcance del MVP. Asimismo, la trazabilidad entre historias de usuario, criterios de aceptación y casos de prueba permite visualizar con claridad qué parte del riesgo funcional fue cubierta durante el ciclo.

### 4.3 Cobertura prevista por HU

| HU | Cobertura principal |
|---|---|
| **HU-01** | creación válida, aforo excedido, información obligatoria incompleta |
| **HU-02** | configuración válida, ventana Early Bird, precios inválidos, cupos mayores al aforo |
| **HU-03** | cartelera visible, tier agotado, Early Bird vencido |
| **HU-04** | compra exitosa, pago rechazado, expiración de reserva, concurrencia en última entrada — la validación de concurrencia incluye verificar que el segundo intento concurrente recibe respuesta de no disponibilidad con código HTTP 409 o equivalente definido por el equipo DEV |
| **HU-05** | liberación por expiración, liberación por pago fallido, disponibilidad visible tras liberación, job de respaldo |
| **HU-06** | notificación de PAYMENT_SUCCESS, PAYMENT_FAILED y RESERVATION_EXPIRED |
| **HU-07** | ticket visible tras compra exitosa, datos correctos, ausencia de ticket si no hubo confirmación |

### 4.3.1 Priorización de HUs por riesgo de negocio

| HU | Nivel de riesgo | Justificación |
|---|---|---|
| **HU-04** | Muy alto | Impacta directamente la reserva, la confirmación de compra, el inventario y la integridad transaccional del MVP |
| **HU-05** | Muy alto | Su fallo bloquea entradas, afecta la disponibilidad real y compromete el valor principal del producto |
| **HU-03** | Alto | Afecta la visibilidad de disponibilidad para el comprador y puede generar decisiones erróneas de compra |
| **HU-02** | Alto | Define reglas comerciales críticas del evento, incluyendo cupos, precios y vigencia de Early Bird |
| **HU-01** | Medio | Habilita la creación base del evento, necesaria para el flujo posterior |
| **HU-06** | Medio | Afecta la comunicación del estado del proceso al comprador |
| **HU-07** | Medio | Valida la evidencia final de compra, pero depende de la correcta ejecución previa del flujo principal |

### 4.4 Matriz de cobertura por historia

| HU | SerenityBDD + Cucumber | Karate | k6 | Validación SQL | Manual / Exploratoria |
|---|---|---|---|---|---|
| **HU-01** | Sí | Sí | No | Sí | Sí |
| **HU-02** | Sí | Sí | No | Sí | Sí |
| **HU-03** | Sí | Sí | Sí, p95 < 400 ms en consulta | No | Sí |
| **HU-04** | Sí | Sí | Sí, p95 < 600 ms en reserva | Sí | Sí |
| **HU-05** | Sí | Sí | No | Sí | Sí |
| **HU-06** | Sí | Sí | No | No | Sí |
| **HU-07** | Sí | Sí | No | Sí | Sí |

**Aclaración sobre k6:** la cobertura marcada con k6 en HU-03 y HU-04 corresponde únicamente a pruebas de rendimiento sobre los flujos críticos de consulta de eventos y creación de reservas. No implica replicar en k6 la totalidad de los casos funcionales definidos en `TEST_CASES.md`, ya que la validación funcional, de reglas de negocio y de estados transaccionales corresponde a la suite de Karate.

**Criterio de cobertura:** todas las HU del MVP tienen cobertura funcional y API. k6 se ejecutará sobre los flujos más sensibles al negocio con umbrales definidos de latencia y TPS. La validación SQL se aplica sobre las HUs que modifican inventario o generan estados transaccionales críticos.

---

## 5. Criterios de Entrada y Salida

### 5.1 Criterios de entrada

- La HU cuenta con criterios de aceptación definidos y revisados.
- El entorno técnico compila, corre y responde.
- Los servicios necesarios del flujo están levantados.
- Los datos de prueba fueron preparados o están disponibles.
- El caso de prueba está documentado en `TEST_CASES.md`.
- Cuando aplique, el caso ya fue registrado como subtarea en GitHub Projects.
- **Para HU-04 y HU-05:** se aplican mecanismos controlados de testability en el backend, permitiendo el disparo manual del proceso de expiración en el entorno de prueba y la verificación complementaria de estados correspondientes sin depender de esperas reales de 10 minutos.

### 5.2 Criterios de salida

- El 100% de los casos de prioridad crítica ejecutados con estado `Pasó`.
- El 100% de los casos de prioridad alta ejecutados con estado `Pasó`.
- No existen defectos críticos abiertos que bloqueen el núcleo del MVP.
- Las evidencias se encuentran disponibles en reportes Karate y documentación de cierre.
- La cobertura de la HU quedó reflejada en reportes, tablero o repositorio.
- El resultado oficial quedó consolidado en `TEST_CASES.md` y `REALITY_CHECK.md`.

---

## 6. Entorno de Pruebas

| Componente | Configuración |
|---|---|
| **ms-events** | Spring Boot — puerto `8081` |
| **ms-ticketing** | Spring Boot — puerto `8082` |
| **ms-notifications** | Spring Boot — puerto `8083` |
| **Mensajería** | RabbitMQ |
| **Base de datos** | PostgreSQL — contenedor definido en `docker-compose` |
| **Orquestación** | Docker + docker-compose |
| **Identidad de prueba** | Usuarios prehabilitados en entorno controlado |
| **Rol** | Validación por contexto controlado / headers de prueba |
| **Pago** | Simulador MOCK con respuesta aprobada o rechazada |
| **Aforo máximo de sala** | Valor acordado con DEV para el entorno de pruebas: **300 entradas**. Este parámetro es configurable por sala; el valor 300 corresponde a la sala de referencia usada en todos los casos de prueba del ciclo MVP. |

---

## 7. Herramientas

| Herramienta | Propósito |
|---|---|
| **SerenityBDD + Cucumber** | Automatización funcional basada en escenarios Gherkin |
| **Karate DSL** | Automatización de pruebas API del sistema |
| **k6** | Pruebas de rendimiento con umbrales de latencia y TPS definidos por flujo |
| **SQL / PostgreSQL client** | Validación directa de consistencia de datos en base de datos como capa de evidencia adicional |
| **Docker / docker-compose** | Levantamiento del entorno reproducible |
| **GitHub Projects** | Gestión del sprint y registro de casos como subtareas |
| **GitHub Issues** | Registro y seguimiento de defectos |
| **Markdown** | Documentación de plan, casos y análisis retrospectivo |

---

## 8. Roles y Responsabilidades

### QA

- Redactar `TEST_PLAN.md`.
- Redactar `TEST_CASES.md`.
- Diseñar la matriz de datos y la cobertura por HU.
- Registrar casos de prueba como subtareas dentro de GitHub Projects.
- Automatizar escenarios funcionales con SerenityBDD + Cucumber.
- Diseñar y ejecutar pruebas de API con Karate.
- Ejecutar pruebas de rendimiento con k6 sobre los flujos críticos.
- Ejecutar validaciones SQL directas sobre PostgreSQL para verificar consistencia de inventario y estados.
- Registrar defectos con evidencia.
- Apoyar la elaboración de `REALITY_CHECK.md`.
- Registrar, junto con el DEV, el tiempo real invertido frente a la estimación original.

### DEV

- Implementar las historias seleccionadas para el MVP.
- Mantener operativo el entorno de ejecución.
- Corregir defectos reportados por QA.
- Apoyar con configuración, datos de prueba y revisión de reglas de negocio.
- Participar en la comparación entre Story Points estimados y tiempo real invertido.
- Entregar un incremento funcional que compile, corra y aporte valor al contexto del negocio.

---

## 9. Cronograma y Estimación

El esfuerzo de QA se organiza por micro-sprints de 2 días, siguiendo la complejidad funcional y los Story Points del backlog priorizado.

| Micro-sprint | HUs | SP | Actividades QA |
|---|---|---:|---|
| **Días 1–2** | HU-01, HU-02 | 10 | diseño de casos, matriz de datos, validación de evento, aforo, tiers, precios y Early Bird |
| **Días 3–4** | HU-03, HU-04 | 11 | validación de cartelera, disponibilidad, reserva, pago simulado, expiración, concurrencia, script k6 y validaciones SQL de inventario |
| **Días 5–6** | HU-05, HU-06, HU-07 | 13 | liberación automática, notificaciones, ticket confirmado, validaciones SQL de estados, consolidación de evidencias y cierre documental |

### Relación esfuerzo QA vs SP

- **HU de 8 SP:** mayor esfuerzo por manejo de tiempo, estados, integridad e inventario.
- **HU de 5 SP:** esfuerzo medio por validaciones de negocio y persistencia.
- **HU de 2–3 SP:** menor esfuerzo relativo, pero con cobertura obligatoria de aceptación y consistencia.

### Registro expectativa vs realidad

Durante cada micro-sprint se registrará el tiempo real invertido por QA y DEV para contrastarlo contra la estimación original en Story Points. Ese contraste se resumirá en `REALITY_CHECK.md` como parte del análisis retrospectivo del proyecto.

---

## 10. Entregables de Prueba

### 10.1 Entregables documentales

- `TEST_PLAN.md`
- `TEST_CASES.md`
- `REALITY_CHECK.md`

### 10.2 Entregables del proyecto y la ejecución

- Repositorio del producto con el MVP funcional.
- Enlace al GitHub Projects actualizado.
- Casos de prueba registrados como subtareas en las HUs.
- Repositorio de pruebas funcionales con SerenityBDD + Cucumber.
- Repositorio de pruebas API del sistema con Karate.
- Scripts o carpeta de rendimiento con k6.
- Evidencias de ejecución y reportes.
- Registro de bugs o incidencias.
- Registro de tiempos reales del micro-sprint o evidencia equivalente para el análisis retrospectivo.
- **Matriz de trazabilidad AC → Caso de prueba → Estado:** documento Markdown que vincula cada criterio de aceptación con su caso de prueba correspondiente y el resultado de ejecución, actualizado al cierre de cada micro-sprint y consolidado al cierre del ciclo MVP.

### 10.3 Entregable técnico adicional

- Repositorio independiente de Karate con **4 escenarios** (`GET`, `POST`, `PUT`, `DELETE`) apuntando a `automationexercise.com/api_list`, con `README.md` de ejecución.

---

## 11. Riesgos y Contingencias

### 11.1 Riesgos de producto

| Riesgo | Probabilidad | Impacto | Mitigación |
|---|:---:|:---:|---|
| Compra simultánea sobre la última entrada disponible | Alta | Alto | Priorizar pruebas de concurrencia en HU-04; validar que el segundo intento concurrente retorna HTTP 409 o equivalente y no genera sobreventa |
| Reserva no liberada tras expiración o pago fallido | Alta | Alto | Cubrir liberación automática y proceso de respaldo en HU-05 |
| Early Bird visible fuera de vigencia | Media | Alto | Probar ventanas temporales en HU-02 y HU-03 |
| Ticket generado sin compra confirmada | Media | Alto | Validar integridad entre pago, reserva y ticket en HU-04 y HU-07; confirmar con validación SQL directa sobre la base de datos |
| Notificación incorrecta o ausente | Media | Medio | Casos específicos de PAYMENT_SUCCESS, PAYMENT_FAILED y RESERVATION_EXPIRED |
| Aforo del evento superior a la capacidad de la sala | Media | Alto | Casos de validación de negocio en HU-01; el límite de sala usado en pruebas es 300 entradas según acuerdo con DEV |

### 11.2 Riesgos de proyecto

| Riesgo | Probabilidad | Impacto | Mitigación |
|---|:---:|:---:|---|
| Entorno no disponible al iniciar el micro-sprint | Media | Alto | Ejecutar smoke test técnico antes del ciclo formal |
| Desfase entre Story Points y tiempo real | Alta | Medio | Registrar tiempos reales y documentarlo en `REALITY_CHECK.md` |
| Temporizador real de 10 minutos vuelve lentas las pruebas | Alta | Medio | Uso de mecanismos de testability en backend y disparo manual del proceso de expiración en entorno de prueba — criterio de entrada obligatorio |
| HU incompletas al inicio del sprint | Media | Alto | Aplicar criterios de entrada estrictos y re-priorizar si es necesario |
| Diferencia entre timer visible y reloj del servidor | Media | Medio | Validar expiración contra estado real del backend y no solo contra el temporizador visible |

---

## 12. Definiciones y Convenciones

### 12.1 Prioridad de casos de prueba

- **Crítico:** afecta directamente el núcleo del MVP o la entrega de valor al negocio.
- **Alto:** afecta una regla importante, pero existe una vía parcial de continuidad.
- **Medio:** afecta validaciones secundarias o mensajes no bloqueantes.
- **Bajo:** impacto menor, cosmético o de mejora.

### 12.2 Severidad de defectos

- **Crítica:** bloquea el flujo principal, genera inconsistencia de inventario, sobreventa o impide completar el MVP.
- **Alta:** afecta una funcionalidad importante del sprint, pero no inutiliza todo el sistema.
- **Media:** defecto funcional acotado con workaround temporal.
- **Baja:** problema visual, de texto o mejora no bloqueante.

### 12.3 Convención para TEST_CASES.md

Los campos **Resultado obtenido** y **Estado** se registran inicialmente como **"Sin ejecutar"** y se actualizan a su estatus definitivo (ej. `Pasó`) al cierre de la ejecución de la suite automatizada real. Los casos deben quedar vinculados como subtareas dentro de su HU correspondiente en GitHub Projects.

### 12.4 Convención de reporte de bug

```text
ID: BUG-XXX
HU: HU-0X
Severidad: Crítica | Alta | Media | Baja
Título: [Descripción breve]
Precondiciones: [Estado del sistema]
Pasos: 1. ... 2. ... 3. ...
Resultado esperado: [Según HU / criterio]
Resultado obtenido: [Comportamiento real]
Evidencia: [captura, video, log o reporte]
Entorno: [local / QA / docker]
```

---

## 13. Cierre

Este plan define el alcance, la estrategia y los criterios de calidad para el ciclo de pruebas del MVP. Su propósito es garantizar que el núcleo funcional del sistema se valide con trazabilidad y criterio profesional, asegurando que cada historia de usuario entregue el valor de negocio para el que fue diseñada.

### 13.1 Estado de ejecución del ciclo

- Se ejecutaron los 29 casos de prueba definidos para el ciclo MVP.
- Los 29 casos finalizaron exitosamente con estado `Pasó`.
- Se logró una cobertura final de 7 HUs y 24 criterios de aceptación.
- La evidencia formal técnica está disponible en los reportes de Karate y en la documentación del proyecto.
- El cierre de ejecución quedó documentado y consolidado en `TEST_CASES.md` y `REALITY_CHECK.md`.

**Redactado por:** Christopher Ismael Pallo Arias — QA
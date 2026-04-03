# TEST_PLAN.md
## Ticketing MVP
 
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
| **API** | Karate | Validar contratos, códigos HTTP, estructura JSON y reglas de negocio de los servicios |
| **Rendimiento básico** | k6 | Ejecutar pruebas básicas de carga sobre los flujos más sensibles del sistema: disponibilidad y reserva |
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

### 4.3 Cobertura prevista por HU
 
| HU | Cobertura principal |
|---|---|
| **HU-01** | creación válida, aforo excedido, información obligatoria incompleta |
| **HU-02** | configuración válida, ventana Early Bird, precios inválidos, cupos mayores al aforo |
| **HU-03** | cartelera visible, tier agotado, Early Bird vencido |
| **HU-04** | compra exitosa, pago rechazado, expiración de reserva, concurrencia en última entrada — la validación de concurrencia incluye verificar que el segundo intento concurrente recibe respuesta de no disponibilidad con código HTTP 409 o equivalente definido por el equipo DEV |
| **HU-05** | liberación por expiración, liberación por pago fallido, disponibilidad visible tras liberación, job de respaldo |
| **HU-06** | notificación por compra exitosa, rechazo de pago y liberación por expiración |
| **HU-07** | ticket visible tras compra exitosa, datos correctos, ausencia de ticket si no hubo confirmación |

### 4.4 Matriz de cobertura por historia
 
| HU | SerenityBDD + Cucumber | Karate | k6 | Manual / Exploratoria |
|---|---|---|---|---|
| **HU-01** | Sí | Sí | No | Sí |
| **HU-02** | Sí | Sí | No | Sí |
| **HU-03** | Sí | Sí | Sí, carga ligera en consulta | Sí |
| **HU-04** | Sí | Sí | Sí, carga ligera en reserva | Sí |
| **HU-05** | Sí | Sí | No | Sí |
| **HU-06** | Sí | Sí | No | Sí |
| **HU-07** | Sí | Sí | No | Sí |
 
**Criterio de cobertura:** todas las HU del MVP tienen cobertura funcional y API; k6 se aplicará al menos sobre los flujos más sensibles al negocio: visualización de disponibilidad y reserva temporal.
 
---

## 5. Criterios de Entrada y Salida
 
### 5.1 Criterios de entrada
 
- La HU cuenta con criterios de aceptación definidos y revisados.
- El entorno técnico compila, corre y responde.
- Los servicios necesarios del flujo están levantados.
- Los datos de prueba fueron preparados o están disponibles.
- El caso de prueba está documentado en `TEST_CASES.md`.
- Cuando aplique, el caso ya fue registrado como subtarea en GitHub Projects.
- **Para HU-04 y HU-05:** el temporizador de reserva está configurado en modo controlado o con mock que permita acelerar la expiración sin depender de esperas reales de 10 minutos.
 
### 5.2 Criterios de salida
 
- El **100% de los casos de prioridad Crítica** de la HU quedaron ejecutados con estado Pasó, o documentados formalmente con estado Sin ejecutar si el entregable es solo documental en este ciclo.
- El **80% o más de los casos de prioridad Alta** de la HU quedaron ejecutados con estado Pasó.
- No existen defectos críticos abiertos que bloqueen el núcleo del MVP.
- Se cuenta con evidencia de ejecución, reporte o registro del estado del caso.
- La cobertura de la HU quedó reflejada en reportes, tablero o repositorio.
- El resultado del ciclo queda resumido en `REALITY_CHECK.md` al cierre del sprint.
 
---
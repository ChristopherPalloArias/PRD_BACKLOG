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
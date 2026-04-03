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
 
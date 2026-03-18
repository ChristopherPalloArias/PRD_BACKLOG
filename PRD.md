  # PRD — Sistema de Venta de Entradas para Obras de Teatro
  
  ## 1. Visión y Objetivos

### 1.1 Problema que resuelve

Actualmente, los eventos teatrales limitan su potencial de ingresos debido a dos barreras principales. Primero, la dependencia de canales de venta presenciales reduce la ventana de compra a horarios de oficina y excluye a clientes que, por falta de tiempo o movilidad, desisten de asistir. Segundo, cuando el usuario intenta comprar en línea, las plataformas actuales presentan una limitación: no liberan automáticamente las entradas si un pago no se completa, bloqueando el inventario de forma indefinida.

Esta combinación de presencialidad y mala gestión digital genera una doble frustración: el comprador se enfrenta a funciones falsamente 'agotadas', y el organizador pierde ventas potenciales. El resultado final es una fuga constante de ingresos y de audiencia.
 
### 1.2 Propuesta de valor

Un sistema de ticketing ágil que asegura la disponibilidad real mediante un temporizador estricto de reserva de 10 minutos y la liberación automática de entradas ante fallos de pago. Al llevar la gestión al entorno digital de forma eficiente, la plataforma permite a los organizadores configurar el aforo por evento, definir precios por categorías (VIP, General, Early Bird) y maximizar la ocupación de la sala. Para el comprador, esto elimina la frustración y se traduce en transparencia: si una entrada aparece disponible, lo está.

### 1.3 Actores del sistema

- **Administrador:** crea eventos, configura aforo, define tiers y precios.
- **Comprador:** consulta disponibilidad, reserva entradas, realiza pago simulado y visualiza su ticket confirmado.

### 1.4 Objetivos del MVP 

| Objetivo | KPI de éxito |
| --- | --- |
| Reducir el bloqueo inútil de entradas por fallos de pago o timeouts | 99.9% de reservas no pagadas liberadas en ≤ 10 minutos |
| Impulsar ventas tempranas | 100% del tier Early Bird agotado antes de su fecha de caducidad |
| Evitar la sobreventa | 0 reportes de entradas duplicadas para una misma obra |
| Garantizar una experiencia de compra fluida | Flujo de compra completo en ≤ 5 minutos |
| Brindar visibilidad de disponibilidad en tiempo real | Tasa de abandono al seleccionar entradas ≤ 10% |

 ## 2. Alcance del MVP

 ### 2.1 IN scope

- Uso del sistema en un contexto controlado con usuarios preexistentes o acceso previamente habilitado para administrador y comprador.
- Creación de eventos con aforo configurable por el administrador
- Validación de que el aforo no supere el máximo permitido del venue
- Configuración de tiers por evento: VIP, General y Early Bird
- Definición de cupos por tier, respetando que la suma total no supere el aforo del evento
- Definición de precios por tier por evento
- Ventana de vigencia por tiempo para el tier Early Bird
- Visualización de eventos disponibles para compra
- Visualización de disponibilidad por tier en tiempo real
- Flujo de reserva de entradas con temporizador de 10 minutos
- Simulación de pasarela de pago con resultado exitoso o fallido
- Liberación automática de entradas cuando el pago falla
- Liberación automática de entradas cuando expira la reserva
- Notificaciones inmediatas al comprador dentro del sistema en caso de compra exitosa, pago fallido o liberación de la entrada
- Visualización del ticket confirmado después de una compra exitosa


### 2.2 OUT scope

- Registro de administrador
- Registro de comprador
- Inicio de sesión para usuarios
- Pasarela de pago real
- Cancelaciones y reembolsos por parte del comprador
- Reportes y métricas de ventas para el administrador
- App móvil nativa
- Soporte multilenguaje
- Integración con correo o mensajería real
- Selección avanzada de asientos numerados
- Promociones distintas a Early Bird

## 3. Reglas de negocio y supuestos

### 3.1 Reglas de negocio

- El sistema maneja dos roles: **Administrador** y **Comprador**.
- El acceso y cambio de roles se gestiona a través del contexto controlado de usuarios preexistentes, sin validación de credenciales reales ni contraseñas.
- El administrador configura el aforo del evento y este no puede superar el máximo de la sala.
- Cada evento puede tener hasta tres tiers: **VIP**, **General** y **Early Bird**.
- El tier **Early Bird** está disponible solo dentro de una ventana de tiempo definida por el administrador.
- Los precios se configuran por tier y por evento.
- La suma de cupos asignados a los tiers no puede superar el aforo total del evento.
- Una reserva tiene una vigencia máxima de **10 minutos** para completar el pago.
- Si el pago falla o la reserva expira, las entradas deben liberarse automáticamente.
- Las notificaciones al comprador deben emitirse inmediatamente después del resultado relevante.
- El pago es simulado dentro del MVP.
- El ticket confirmado solo se genera cuando la compra ha sido exitosa.
- No se contemplan reembolsos ni cancelaciones en esta primera versión.

### 3.2 Supuestos

- El sistema procesa pagos simulados únicamente en dólares.
- Los eventos publicados son visibles para todos los compradores sin la necesidad de utilizar filtros.
- La disponibilidad de entradas que ve el comprador corresponde al inventario real del sistema.
- La reserva expira según el reloj del servidor, no del comprador.
- El ticket confirmado solo se genera cuando el pago ha sido exitoso.
- Para el alcance de este MVP, se asume un entorno controlado con usuarios previamente habilitados, por lo que el registro y el inicio de sesión no forman parte de esta versión inicial.

# PRD — Sistema de Venta de Entradas para Obras de Teatro
  
## 1. Visión y Objetivos

### 1.1 Problema que resuelve

Actualmente, los eventos teatrales limitan su potencial de ingresos debido a dos barreras principales. Primero, la dependencia de canales de venta presenciales reduce la ventana de compra a horarios de oficina y excluye a clientes que, por falta de tiempo o movilidad, desisten de asistir. Segundo, cuando el usuario intenta comprar en línea, las plataformas actuales presentan una limitación: no liberan automáticamente las entradas si un pago no se completa, bloqueando el inventario de forma indefinida.

Esta combinación de presencialidad y mala gestión digital genera una doble frustración: el comprador se enfrenta a funciones falsamente 'agotadas', y el organizador pierde ventas potenciales. El resultado final es una perdida constante de ingresos y de audiencia.
 
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
- Validación de que el aforo no supere el máximo permitido de la sala
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
- Los eventos son visibles para todos los compradores sin necesidad de utilizar filtros.
- La disponibilidad de entradas que ve el comprador corresponde al inventario real del sistema.
- La reserva expira según el reloj del servidor, no del comprador.
- El ticket confirmado solo se genera cuando el pago ha sido exitoso.
- Para el alcance de este MVP, se asume un entorno controlado con usuarios previamente habilitados, por lo que el registro y el inicio de sesión no forman parte de esta versión inicial.

## 4. Riesgos

### 4.1 Riesgos de negocio

| Riesgo | Probabilidad | Impacto | Mitigación |
| --- | --- | --- | --- |
| Pago procesado pero la compra no se refleja para el comprador | Media | Alto | El sistema registra el estado de cada transacción y confirma la compra solo cuando el pago es exitoso |
| Dos compradores adquieren la misma entrada simultáneamente | Alta | Alto | Se verifica disponibilidad en el momento exacto de la confirmación, garantizando que solo un comprador pueda completar la compra. |
| Sobreventa por fallo en control de inventario en tiempo real | Media | Alto | La disponibilidad se consulta en tiempo real antes de cualquier confirmación, garantizando que solo un comprador pueda completar la compra |
| Administrador configura aforo superior al máximo de la sala | Baja | Alto | El sistema bloquea la configuración si el aforo ingresado supera la capacidad máxima registrada para la sala. |
| Early Bird no se desactiva al vencer la ventana de tiempo | Media | Alto | El scheduler monitorea las ventanas de tiempo y desactiva el tier cuando corresponde, sin intervención manual. |
| El simulador de pago rechaza intentos válidos y el comprador abandona la compra | Alta | Medio | Se muestran mensajes claros del error y se permite reintentar mientras la reserva siga vigente. |
| Baja demanda en tier VIP | Media | Bajo | Monitorear métricas y ajustar estrategias de precios o promoción si es necesario |

### 4.2 Riesgos técnicos

| Riesgo | Probabilidad | Impacto | Mitigación |
| --- | --- | --- | --- |
| Condiciones de carrera al comprar la última entrada simultáneamente | Alta | Alto | Se aplica bloqueo optimista en base de datos para garantizar que solo una transacción pueda completarse |
| Fallo de pago sin notificación al comprador | Media | Alto | Cada transacción queda registrada y el comprador recibe una notificación sin importar el resultado |
| Caída del scheduler y las entradas quedan bloqueadas indefinidamente | Baja | Alto | Un job de respaldo escanea periódicamente reservas vencidas y las libera si el scheduler principal falla |
| Latencia hace que el timer del front difiera del back | Media | Medio | El temporizador que ve el comprador es orientativo, la vigencia real siempre la determina el servidor |
| Servidor cae con el timer activo y la reserva queda en el limbo | Baja | Alto | El estado y los timestamps de cada reserva se persisten en base de datos para poder recuperarlos al reiniciar |
| Notificaciones duplicadas por reintentos de red | Baja | Bajo | Se acepta el riesgo con manejo básico de idempotencia para evitar envíos repetidos |
| Inconsistencias entre estado de pago y estado de ticket | Media | Alto | El ticket solo se emite tras validar que el estado del pago y el de la compra son consistentes entre sí |

## 5. Criterios de éxito del MVP

El MVP se considerará exitoso si permite:

- Crear y configurar eventos con aforo, tiers y precios válidos
- Mostrar disponibilidad real por tier para los compradores
- Completar el flujo de reserva y pago simulado sin duplicidad de entradas
- Liberar automáticamente entradas no pagadas en un máximo de 10 minutos
- Notificar correctamente al comprador en los eventos principales del flujo
- Generar ticket únicamente en compras exitosas

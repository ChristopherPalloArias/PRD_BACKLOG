  # Subtasks y Estimación — Sistema de Venta de Entradas
> Escala de estimación: Fibonacci (1, 2, 3, 5, 8, 13)
---
## HU-01: Creación de evento de obra de teatro — SP: 5
#### **Justificación SP:** Historia de complejidad media. Requiere persistencia, validaciones de negocio, control por rol y cobertura de pruebas de camino feliz y límites.
### DEV

- [ ] Crear entidad y tabla de eventos
- [ ] Implementar endpoint o servicio de creación de eventos
- [ ] Validar información obligatoria del evento
- [ ] Validar aforo contra el máximo permitido de la sala
- [ ] Persistir evento con la información ingresada
- [ ] Restringir creación a usuarios con rol administrador
### QA
- [ ] Diseñar matriz de datos válidos e inválidos para creación de eventos
- [ ] Ejecutar prueba de creación exitosa con aforo permitido
- [ ] Ejecutar prueba de rechazo por aforo superior al máximo
- [ ] Ejecutar prueba de rechazo por información mínima incompleta
- [ ] Verificar que el evento quede registrado correctamente al crearse
---

## HU-02: Configuración de tiers y precios por evento — SP: 5
#### **Justificación SP:** Complejidad media. Agrega reglas cruzadas entre precios, cupos, aforo y vigencia temporal, por lo que requiere mayor cobertura funcional y de consistencia.
### DEV

- [ ] Crear entidad y tabla de tiers asociada al evento
- [ ] Implementar endpoint o servicio de configuración comercial
- [ ] Validar tipos permitidos de tier: VIP, General y Early Bird
- [ ] Validar precios mayores a cero
- [ ] Validar cupos asignados por tier
- [ ] Validar que la suma de cupos no supere el aforo del evento
- [ ] Implementar vigencia temporal del tier Early Bird
- [ ] Permitir guardar la configuración comercial del evento
### QA
- [ ] Diseñar matriz de datos para combinaciones de tiers, precios y cupos
- [ ] Validar configuración exitosa de VIP, General y Early Bird
- [ ] Validar vigencia correcta del Early Bird dentro del período definido
- [ ] Validar rechazo por precio igual a cero o negativo
- [ ] Validar rechazo por suma de cupos mayor al aforo
- [ ] Verificar que la configuración válida quede correctamente almacenada
---

## HU-03: Visualización de eventos y disponibilidad — SP: 3
#### **Justificación SP:** Historia de consulta con menor complejidad técnica que las transaccionales, pero con reglas de negocio claras sobre visibilidad y disponibilidad.
### DEV

- [ ] Implementar consulta de eventos disponibles
- [ ] Implementar consulta de disponibilidad por tier
- [ ] Filtrar eventos sin entradas disponibles
- [ ] Excluir tiers agotados de la disponibilidad activa
- [ ] Excluir Early Bird fuera de vigencia
- [ ] Presentar disponibilidad vigente por tier
### QA
- [ ] Diseñar datos de prueba para eventos con y sin entradas disponibles
- [ ] Validar visualización de eventos con entradas disponibles
- [ ] Validar que un tier agotado aparezca como no disponible
- [ ] Validar que Early Bird vencido no se muestre como opción disponible
- [ ] Verificar que solo se muestre disponibilidad vigente por tier
---

## HU-04: Reserva y compra de entrada con pago simulado — SP: 8
#### **Justificación SP:** Historia de alta complejidad. Combina manejo de estados, tiempo límite, inventario, concurrencia y consistencia de datos.
### DEV

- [ ] Crear entidad y tabla de reservas con estado y timestamp
- [ ] Implementar creación de reserva para un tier disponible
- [ ] Implementar servicio o endpoint de pago simulado
- [ ] Validar disponibilidad real antes de reservar
- [ ] Confirmar compra ante pago exitoso dentro del tiempo permitido
- [ ] Descontar inventario al confirmar la compra
- [ ] Evitar confirmación de compras sobre reservas vencidas
- [ ] Asociar compra confirmada con ticket emitido
- [ ] Manejar rechazo de pago sin confirmar la entrada
### QA
- [ ] Diseñar matriz de datos para reserva y pago simulado
- [ ] Ejecutar prueba de compra exitosa dentro del tiempo permitido
- [ ] Ejecutar prueba de compra fallida por pago rechazado
- [ ] Ejecutar prueba de expiración de reserva luego de 10 minutos
- [ ] Ejecutar prueba de doble intento sobre la última entrada disponible
- [ ] Verificar que una compra confirmada descuente inventario y genere ticket
---
## HU-05: Liberación automática por fallo de pago o expiración — SP: 8
#### **Justificación SP:** Historia de alta complejidad. El sistema debe ser capaz de actuar solo, en segundo plano y sin margen de error, garantizando que ninguna entrada quede bloqueada ni se libere por equivocación.
### DEV
- [ ] Implementar detección de reservas vencidas
- [ ] Liberar automáticamente entradas de reservas expiradas
- [ ] Liberar automáticamente entradas de pagos rechazados
- [ ] Actualizar estado de la reserva luego de la liberación
- [ ] Reflejar nuevamente la entrada en disponibilidad
- [ ] Implementar proceso de respaldo para reservas no liberadas por el mecanismo principal
- [ ] Evitar liberación sobre compras ya confirmadas
### QA
- [ ] Diseñar datos de prueba para reservas expiradas y pagos rechazados
- [ ] Ejecutar prueba de liberación automática por expiración
- [ ] Ejecutar prueba de liberación automática por pago rechazado
- [ ] Verificar que la entrada liberada vuelva a aparecer disponible
- [ ] Ejecutar prueba de regularización por proceso de respaldo
- [ ] Verificar que una compra confirmada no sea liberada erróneamente
---
## HU-06: Notificaciones al comprador — SP: 3
#### **Justificación SP:** Historia pequeña-media. Tiene pocos flujos principales, pero depende de eventos del sistema y requiere control de duplicidad y trazabilidad.
### DEV
- [ ] Implementar servicio simulado de notificaciones
- [ ] Enviar notificación al confirmar compra
- [ ] Enviar notificación al rechazar pago
- [ ] Enviar notificación al liberar una reserva expirada
- [ ] Asociar el motivo correcto a cada notificación emitida
### QA
- [ ] Diseñar datos de prueba para eventos de notificación
- [ ] Validar notificación por compra exitosa
- [ ] Validar notificación por pago fallido
- [ ] Validar notificación por liberación de reserva
- [ ] Verificar correspondencia entre evento del sistema y mensaje emitido
---
## HU-07: Visualización de ticket confirmado — SP: 2
**Justificación SP:** Historia pequeña de consulta, pero con control de acceso e integridad de datos como aspectos críticos.
### DEV
- [ ] Implementar consulta de ticket confirmado por compra
- [ ] Mostrar datos del evento, tier y compra
- [ ] Permitir visualización solo para compras confirmadas
- [ ] Restringir acceso al ticket al comprador propietario
### QA
- [ ] Diseñar datos de prueba para tickets confirmados y no confirmados
- [ ] Validar visualización de ticket luego de compra exitosa
- [ ] Validar información correcta mostrada en el ticket
- [ ] Validar ausencia de ticket para compra no confirmada
- [ ] Verificar acceso solo del propietario al ticket
---

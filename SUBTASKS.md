  # Subtasks y Estimación — Sistema de Venta de Entradas

---

## HU-01: Creación de evento de obra de teatro — SP: 5

### DEV

- Crear entidad y tabla de eventos
- Implementar endpoint o servicio de creación de eventos
- Validar información obligatoria del evento
- Validar aforo contra el máximo permitido de la sala
- Persistir evento en estado borrador
- Restringir creación a usuarios con rol administrador
---

## HU-02: Configuración de tiers y precios por evento — SP: 5

### DEV

- Crear entidad y tabla de tiers asociada al evento
- Implementar endpoint o servicio de configuración comercial
- Validar tipos permitidos de tier: VIP, General y Early Bird
- Validar precios mayores a cero
- Validar cupos asignados por tier
- Validar que la suma de cupos no supere el aforo del evento
- Implementar vigencia temporal del tier Early Bird
- Permitir guardar configuración comercial del evento en borrador
---

## HU-03: Visualización de eventos y disponibilidad — SP: 3

### DEV

- Implementar consulta de eventos publicados
- Implementar consulta de disponibilidad por tier
- Filtrar eventos no publicados
- Excluir tiers agotados de la disponibilidad activa
- Excluir Early Bird fuera de vigencia
- Presentar disponibilidad vigente por tier
---

## HU-04: Reserva y compra de entrada con pago simulado — SP: 8

### DEV

- Crear entidad y tabla de reservas con estado y timestamp
- Implementar creación de reserva para un tier disponible
- Implementar servicio o endpoint de pago simulado
- Validar disponibilidad real antes de reservar
- Confirmar compra ante pago exitoso dentro del tiempo permitido
- Descontar inventario al confirmar la compra
- Evitar confirmación de compras sobre reservas vencidas
- Asociar compra confirmada con ticket emitido
- Manejar rechazo de pago sin confirmar la entrada
---

## HU-05: Liberación automática por fallo de pago o expiración — SP: 8

### DEV Funcional

- Implementar detección de reservas vencidas
- Liberar automáticamente entradas de reservas expiradas
- Liberar automáticamente entradas de pagos rechazados
- Actualizar estado de la reserva luego de la liberación
- Reflejar nuevamente la entrada en disponibilidad
- Implementar proceso de respaldo para reservas no liberadas por el mecanismo principal
- Evitar liberación sobre compras ya confirmadas

### DEV No Funcional

- Programar scheduler o job periódico de verificación
- Registrar logs de liberación automática y reproceso
- Manejar fallos silenciosos del proceso principal
- Asegurar idempotencia básica del reproceso
- Proteger consistencia del inventario ante ejecuciones repetidas
  # Subtasks y Estimación — Sistema de Venta de Entradas

---

## HU-01: Creación de evento de obra de teatro — SP: 5

### DEV Funcional

- Crear entidad y tabla de eventos
- Implementar endpoint o servicio de creación de eventos
- Validar información obligatoria del evento
- Validar aforo contra el máximo permitido de la sala
- Persistir evento en estado borrador
- Restringir creación a usuarios con rol administrador

### DEV No Funcional

- Implementar validaciones de integridad de entrada en backend
- Registrar logs básicos de creación de eventos
- Manejar errores de validación sin exponer detalles sensibles
- Asegurar consistencia transaccional para evitar registros parciales

---

## HU-02: Configuración de tiers y precios por evento — SP: 5

### DEV Funcional

- Crear entidad y tabla de tiers asociada al evento
- Implementar endpoint o servicio de configuración comercial
- Validar tipos permitidos de tier: VIP, General y Early Bird
- Validar precios mayores a cero
- Validar cupos asignados por tier
- Validar que la suma de cupos no supere el aforo del evento
- Implementar vigencia temporal del tier Early Bird
- Permitir guardar configuración comercial del evento en borrador

### DEV No Funcional

- Asegurar integridad referencial entre evento y tiers
- Registrar logs de cambios en configuración de tiers y precios
- Manejar errores de configuración de forma consistente
- Validar consistencia de fechas para la vigencia de Early Bird

---

## HU-03: Visualización de eventos y disponibilidad — SP: 3

### DEV Funcional

- Implementar consulta de eventos publicados
- Implementar consulta de disponibilidad por tier
- Filtrar eventos no publicados
- Excluir tiers agotados de la disponibilidad activa
- Excluir Early Bird fuera de vigencia
- Presentar disponibilidad vigente por tier

### DEV No Funcional

- Optimizar consultas de cartelera y disponibilidad
- Manejar respuestas vacías y errores de consulta
- Registrar métricas básicas de uso de la consulta

---

## HU-04: Reserva y compra de entrada con pago simulado — SP: 8

### DEV Funcional

- Crear entidad y tabla de reservas con estado y timestamp
- Implementar creación de reserva para un tier disponible
- Implementar servicio o endpoint de pago simulado
- Validar disponibilidad real antes de reservar
- Confirmar compra ante pago exitoso dentro del tiempo permitido
- Descontar inventario al confirmar la compra
- Evitar confirmación de compras sobre reservas vencidas
- Asociar compra confirmada con ticket emitido
- Manejar rechazo de pago sin confirmar la entrada
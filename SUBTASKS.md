  # Subtasks y Estimación — Sistema de Venta de Entradas

## HU-01: Creación de evento de obra de teatro — SP: 5

### DEV Funcional

- [ ] Crear entidad y tabla de eventos
- [ ] Implementar endpoint o servicio de creación de eventos
- [ ] Validar información obligatoria del evento
- [ ] Validar aforo contra el máximo permitido de la sala
- [ ] Persistir evento en estado borrador
- [ ] Restringir creación a usuarios con rol administrador

### DEV No Funcional

- [ ] Implementar validaciones de integridad de entrada en backend
- [ ] Registrar logs básicos de creación de eventos
- [ ] Manejar errores de validación sin exponer detalles sensibles
- [ ] Asegurar consistencia transaccional para evitar registros parciales

## HU-02: Configuración de tiers y precios por evento — SP: 5

### DEV Funcional

- [ ] Crear entidad y tabla de tiers asociada al evento
- [ ] Implementar endpoint o servicio de configuración comercial
- [ ] Validar tipos permitidos de tier: VIP, General y Early Bird
- [ ] Validar precios mayores a cero
- [ ] Validar cupos asignados por tier
- [ ] Validar que la suma de cupos no supere el aforo del evento
- [ ] Implementar vigencia temporal del tier Early Bird
- [ ] Permitir guardar configuración comercial del evento en borrador

### DEV No Funcional

- [ ] Asegurar integridad referencial entre evento y tiers
- [ ] Registrar logs de cambios en configuración de tiers y precios
- [ ] Manejar errores de configuración de forma consistente
- [ ] Validar consistencia de fechas para la vigencia de Early Bird
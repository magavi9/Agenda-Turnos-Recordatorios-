# 🗺️ Mapa del Sistema: Agenda + Recordatorios para Profesionales

## 1. Módulos y Vistas
* **Portal del Paciente (Mobile-First):**
  * Stepper de reserva: Selección de fecha -> Selección de slot libre -> Formulario (Nombre, Celular) -> Confirmación.
* **Dashboard del Profesional (Desktop):**
  * Métricas del día (Turnos, Confirmados, Pendientes, Cancelados).
  * Calendario interactivo semanal con código de colores.
  * Modal para bloqueo rápido de horarios/días.

## 2. Base de Datos (PostgreSQL)
* Tablas: `profesionales`, `horarios_atencion`, `bloqueos_agenda`, `pacientes`, `turnos`, `lista_espera`, `recordatorios_log`.
* Estados de turno: `pendiente`, `confirmado`, `cancelado`, `completado`, `no_asistio`.

## 3. Automatizaciones y Lógica Clave
* **Cálculo de slots:** Cruce de horario habitual, bloqueos y turnos tomados.
* **Transacción concurrente:** Bloqueo de fila para evitar doble reserva simultánea.
* **Cron Job:** Disparo de recordatorios automáticos 24 hs antes de la cita.
* **Webhook WhatsApp:** 
  * Acción CONFIRMAR -> Pasa turno a `confirmado`.
  * Acción CANCELAR -> Pasa turno a `cancelado` y dispara oferta a la `lista_espera`.

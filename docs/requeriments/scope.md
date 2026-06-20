# Scope del Proyecto — Bankify

## 1. Sistema

Bankify es una plataforma digital fintech en etapa de Producto Mínimo Viable (MVP)
para la gestión básica de cuentas bancarias. Permite a clientes finales consultar
información de sus cuentas y realizar operaciones simples, mientras que el personal
interno (Asesores, Supervisores, Gerente Financiero) gestiona clientes, cuentas y
reportes tributarios.

> Pauta: aquí describan en 1 párrafo qué ES el sistema (no qué problema resuelve,
> eso va en la siguiente sección). Mencionen que es un MVP y su naturaleza fintech.

## 2. Problema a Resolver

Actualmente Bankify no cuenta con:
- Registro validado de cuentas bancarias
- Consulta de saldo de una cuenta
- Depósitos de dinero controlados
- Reportes tributarios en PDF para clientes
- Envío de reportes a la DIAN en formato JSON

> Pauta: expliquen el impacto de no tener estas funcionalidades (riesgo regulatorio,
> imposibilidad de operar, falta de transparencia para el cliente, etc.).
> Usen la sección "Problema Actual" del PDF como base, pero redactado en sus
> propias palabras y conectado con el objetivo del MVP: "validar el modelo de
> negocio antes de escalar".

## 3. Diagrama de Contexto

![Diagrama de Contexto C4 - Bankify](https://github.com/heverthisday/DOSW_LABORATORIO_3_Hever_Barrera_Nicolas_Prieto_Mabel_Bernal/blob/feature/DOSW-02-proj-scope/docs/images/diagrama%20C4.jpg)

**Enlace al diagrama editable:** [pegar aquí el link de Miro/Lucidchart/draw.io]

### Actores y sistemas identificados:
- **Cliente**: consulta saldo, realiza depósitos, genera su reporte tributario.
- **Asesor**: gestiona cuentas (crear, activar, inactivar, actualizar).
- **Supervisor**: gestiona clientes (crear, activar, inactivar, actualizar, eliminar).
- **Gerente Financiero**: genera el reporte tributario consolidado de todas las cuentas.
- **DIAN** (sistema externo): recibe el reporte tributario en formato JSON.


## 4. Alcance del Sistema

### Incluido en el MVP:
- Autenticación de usuarios (Clientes y Operadores)
- Gestión de clientes y cuentas según reglas de negocio (10 dígitos, banco
  registrado en sistema)
- Consulta de saldo
- Depósitos a cuenta
- Generación de reporte tributario individual (PDF) y consolidado (JSON para DIAN)

### Fuera de alcance (no incluido en esta fase):
> Pauta: piensen qué NO se va a construir todavía — por ejemplo: retiros,
> transferencias entre cuentas, integración bancaria real, app móvil nativa,
> notificaciones push, etc. Esto demuestra capacidad de análisis crítico
> (conecta directamente con la pregunta "d" de la Parte 3 sobre qué NO debería
> ir en el MVP).
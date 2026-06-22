# Scope del Proyecto — Bankify

## 1. Sistema

Bankify es una plataforma digital fintech en etapa de Producto Mínimo Viable (MVP)
para la gestión básica de cuentas bancarias, tambien  Permite a clientes finales consultar
información de sus cuentas y realizar operaciones , mientras que el personal
interno  como los (Asesores, Supervisores, Gerente Financiero) gestiona clientes, cuentas y
reportes tributarios.



## 2. Problema a Resolver

Actualmente Bankify no tiene :
- Registro validado de cuentas bancarias
- Consulta de saldo de una cuenta
- Depósitos de dinero controlados
- Reportes tributarios en PDF para clientes
- Envío de reportes a la DIAN en formato JSON


## 3. Diagrama de Contexto

![Diagrama de Contexto C4 - Bankify](https://github.com/heverthisday/DOSW_LABORATORIO_3_Hever_Barrera_Nicolas_Prieto_Mabel_Bernal/blob/feature/DOSW-02-proj-scope/docs/images/diagrama%20C4.jpg)

**Enlace al diagrama editable:** [https://miro.com/welcomeonboard/UG91cjFoTk02WnVmcnFuckFGUUFJWlB0S3pRUkVaQ3JVRUhibFEzRER5WGt6WWFTd1RlQmovMHZKUGhPbkFRWENwVWZrci81T1VoMmY3Rit5L1JmUlFLYVI1NjdXWWhpdWxwR3FHODArVDgxWTlXTHZKdEU4L1dVUnd3OUdSSHl3VHhHVHd5UWtSM1BidUtUYmxycDRnPT0hdjE=?share_link_id=215316622083]

### Actores y sistemas identificados:
- **Cliente**: consulta saldo, realiza depósitos, genera su reporte tributario.
- **Asesor**: gestiona cuentas (crear, activar, inactivar, actualizar).
- **Supervisor**: gestiona clientes (crear, activar, inactivar, actualizar, eliminar).
- **Gerente Financiero**: genera el reporte tributario consolidado de todas las cuentas.
- **DIAN** (sistema externo): recibe el reporte tributario en formato JSON.


## 4. Alcance del Sistema

### Incluido en el MVP:
- Autenticación de usuarios (Clientes y Operadores)
- Gestión de clientes y cuentas a partir de las  reglas de negocio (10 dígitos, banco
  registrado en sistema)
- Consulta de saldo
- Depósitos a cuenta
- Generación de reporte tributario individual (PDF) y consolidado (JSON para DIAN)


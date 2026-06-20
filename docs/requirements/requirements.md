# Documento de Requerimientos
## Sistema Bancario - DOSW Laboratorio 3

**Equipo:** Hever Barrera, Nicolás Prieto, Mabel Bernal
**Fecha:** 2026-06-20
**Versión:** 1.0

---

## Requerimientos Funcionales

| ID   | Descripción |
|------|-------------|
| RF01 | El sistema debe autenticar usuarios con usuario y contraseña |
| RF02 | El sistema debe registrar y validar cuentas bancarias (10 dígitos, banco registrado) |
| RF03 | El sistema debe permitir consultar el saldo de una cuenta por el cliente |
| RF04 | El sistema debe permitir realizar depósitos a una cuenta |
| RF05 | El sistema debe generar reporte tributario en PDF para el cliente |
| RF06 | El sistema debe enviar reporte a la DIAN en formato JSON |
| RF07 | El sistema debe permitir realizar retiros de una cuenta validando saldo disponible |
| RF08 | El sistema debe permitir transferencias entre cuentas registradas |

## Requerimientos No Funcionales

| ID    | Categoría       | Descripción |
|-------|-----------------|-------------|
| RNF01 | Seguridad       | Autenticación con tokens JWT |
| RNF02 | Disponibilidad  | 99.5% uptime mensual |
| RNF03 | Rendimiento     | Respuesta < 2 segundos por operación |
| RNF04 | Escalabilidad   | Soportar 10.000 usuarios concurrentes |
| RNF05 | Auditabilidad   | Log de todas las transacciones |
| RNF06 | Mantenibilidad  | Cobertura de pruebas unitarias mínima del 80% |

---

## Detalle de Requerimientos

---

### RF01 - Autenticar usuarios

| Código:          | RF01                        |
|------------------|-----------------------------|
| Nombre:          | Autenticar usuarios         |

| Descripción:        | El sistema permite a un usuario registrado iniciar sesión proporcionando sus credenciales. Si son válidas, se genera un token JWT. |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| Cómo se ejecutará:  | El cliente ingresa usuario y contraseña en el formulario de login y el sistema valida las credenciales. |
| Actor principal:    | Cliente |
| Precondiciones:     | El usuario debe estar registrado en el sistema. |

**► DATOS DE ENTRADA**

| Nombre      | Descripción              | Tipo de campo | Reglas / Aplicación                          | Obligatorio |
|-------------|--------------------------|---------------|----------------------------------------------|-------------|
| Usuario     | Nombre de usuario        | Texto         | Mínimo 4 caracteres, sin espacios            | Sí          |
| Contraseña  | Clave secreta del usuario| Contraseña    | Mínimo 8 caracteres, al menos 1 número       | Sí          |

**DATOS DE SALIDA**

| Nombre       | Descripción                  | Tipo de campo | Reglas / Aplicación              | Obligatorio |
|--------------|------------------------------|---------------|----------------------------------|-------------|
| Token JWT    | Token de acceso del usuario  | Texto         | Expira en 30 minutos             | Sí          |
| Mensaje      | Resultado de la operación    | Texto         | "Login exitoso" o mensaje error  | Sí          |

**FLUJO BÁSICO:**

| Paso | Actor   | Descripción                                              | Excepciones |
|------|---------|----------------------------------------------------------|-------------|
| 1    | Cliente | Ingresa usuario y contraseña en el formulario            | -           |
| 2    | Sistema | Valida las credenciales contra la base de datos          | Paso 1A     |
| 3    | Sistema | Genera y retorna token JWT                               | -           |
| 4    | Cliente | Accede al sistema con el token                           | -           |

**FLUJO ALTERNO:**

| Paso | Actor   | Descripción                                              | Excepciones |
|------|---------|----------------------------------------------------------|-------------|
| 1A   | Sistema | Credenciales incorrectas, retorna error 401              | -           |
| 1B   | Sistema | Cuenta bloqueada tras 3 intentos fallidos                | -           |

| Notas y comentarios: | El token JWT debe enviarse en el header Authorization en cada petición posterior. |
|----------------------|-----------------------------------------------------------------------------------|

**ANEXOS**

PROTOTIPOS: Formulario de login con campos usuario y contraseña.

**REGLAS DE NEGOCIO**

| No. | Descripción                                                                 |
|-----|-----------------------------------------------------------------------------|
| 1   | Después de 3 intentos fallidos la cuenta se bloquea por 15 minutos          |
| 2   | El token JWT expira en 30 minutos                                           |
| 3   | Las contraseñas deben almacenarse cifradas con BCrypt                       |

**ABREVIATURAS**

| Abreviatura | Significado                  |
|-------------|------------------------------|
| JWT         | JSON Web Token               |
| RF          | Requerimiento Funcional      |

**HISTORIAL DE REVISIÓN**

| Elaborado por    | Aprobado por | Fecha      | Descripción y Justificación de Cambios |
|------------------|--------------|------------|----------------------------------------|
| CVDS Company     |              | 22/10/2024 |                                        |
| Nicolás Prieto   |              | 20/06/2026 | Creación del requerimiento RF01        |

---

### RF03 - Consultar saldo de una cuenta

| Código:          | RF03                          |
|------------------|-------------------------------|
| Nombre:          | Consultar saldo de una cuenta |

| Descripción:        | El cliente autenticado puede consultar el saldo actual de cualquiera de sus cuentas registradas. |
|---------------------|--------------------------------------------------------------------------------------------------|
| Cómo se ejecutará:  | El cliente selecciona una cuenta desde su panel y el sistema retorna el saldo actualizado. |
| Actor principal:    | Cliente |
| Precondiciones:     | El cliente debe estar autenticado con token JWT válido. |

**► DATOS DE ENTRADA**

| Nombre        | Descripción                  | Tipo de campo | Reglas / Aplicación              | Obligatorio |
|---------------|------------------------------|---------------|----------------------------------|-------------|
| Número cuenta | Identificador de la cuenta   | Numérico      | 10 dígitos, cuenta debe existir  | Sí          |
| Token JWT     | Token de sesión del cliente  | Texto         | Debe ser válido y no expirado    | Sí          |

**DATOS DE SALIDA**

| Nombre                  | Descripción                        | Tipo de campo | Reglas / Aplicación         | Obligatorio |
|-------------------------|------------------------------------|---------------|-----------------------------|-------------|
| Saldo disponible        | Saldo actual de la cuenta          | Decimal       | Dos decimales, no negativo  | Sí          |
| Fecha última transacción| Fecha de la última operación       | Fecha         | Formato DD/MM/YYYY HH:mm    | Sí          |

**FLUJO BÁSICO:**

| Paso | Actor   | Descripción                                                    | Excepciones |
|------|---------|----------------------------------------------------------------|-------------|
| 1    | Cliente | Selecciona la cuenta a consultar                               | -           |
| 2    | Sistema | Verifica que la cuenta pertenece al cliente autenticado        | Paso 2A     |
| 3    | Sistema | Retorna saldo actual y fecha de última transacción             | -           |

**FLUJO ALTERNO:**

| Paso | Actor   | Descripción                                                    | Excepciones |
|------|---------|----------------------------------------------------------------|-------------|
| 2A   | Sistema | La cuenta no pertenece al cliente, retorna error 403           | -           |
| 2B   | Sistema | La cuenta no existe, retorna error 404                         | -           |

| Notas y comentarios: | El saldo debe reflejar todas las transacciones en tiempo real. |
|----------------------|----------------------------------------------------------------|

**ANEXOS**

PROTOTIPOS: Pantalla de detalle de cuenta con saldo y últimos movimientos.

**REGLAS DE NEGOCIO**

| No. | Descripción                                                                 |
|-----|-----------------------------------------------------------------------------|
| 1   | Solo el dueño de la cuenta puede consultar su saldo                         |
| 2   | La respuesta debe entregarse en menos de 2 segundos                         |
| 3   | Se registra en el log cada consulta de saldo realizada                      |

**ABREVIATURAS**

| Abreviatura | Significado                  |
|-------------|------------------------------|
| JWT         | JSON Web Token               |
| RNF         | Requerimiento No Funcional   |

**HISTORIAL DE REVISIÓN**

| Elaborado por    | Aprobado por | Fecha      | Descripción y Justificación de Cambios |
|------------------|--------------|------------|----------------------------------------|
| CVDS Company     |              | 22/10/2024 |                                        |
| Nicolás Prieto   |              | 20/06/2026 | Creación del requerimiento RF03        |

---

### RF04 - Realizar depósitos a una cuenta

| Código:          | RF04                            |
|------------------|---------------------------------|
| Nombre:          | Realizar depósitos a una cuenta |

| Descripción:        | El cliente autenticado puede realizar depósitos de dinero a una cuenta bancaria registrada. |
|---------------------|---------------------------------------------------------------------------------------------|
| Cómo se ejecutará:  | El cliente selecciona la cuenta destino, ingresa el monto y confirma la operación. |
| Actor principal:    | Cliente |
| Precondiciones:     | El cliente debe estar autenticado y la cuenta destino debe existir. |

**► DATOS DE ENTRADA**

| Nombre        | Descripción                   | Tipo de campo | Reglas / Aplicación                    | Obligatorio |
|---------------|-------------------------------|---------------|----------------------------------------|-------------|
| Número cuenta | Cuenta destino del depósito   | Numérico      | 10 dígitos, cuenta debe existir        | Sí          |
| Monto         | Valor a depositar             | Decimal       | Mayor a 0, máximo 2 decimales          | Sí          |
| Token JWT     | Token de sesión del cliente   | Texto         | Debe ser válido y no expirado          | Sí          |

**DATOS DE SALIDA**

| Nombre               | Descripción                         | Tipo de campo | Reglas / Aplicación              | Obligatorio |
|----------------------|-------------------------------------|---------------|----------------------------------|-------------|
| Comprobante          | Confirmación de la transacción      | Texto         | Número de transacción único      | Sí          |
| Nuevo saldo          | Saldo actualizado tras el depósito  | Decimal       | Dos decimales, no negativo       | Sí          |

**FLUJO BÁSICO:**

| Paso | Actor   | Descripción                                                    | Excepciones |
|------|---------|----------------------------------------------------------------|-------------|
| 1    | Cliente | Selecciona cuenta destino e ingresa el monto                   | -           |
| 2    | Sistema | Valida que el monto sea mayor a cero                           | Paso 2A     |
| 3    | Sistema | Verifica que la cuenta destino existe                          | Paso 3A     |
| 4    | Sistema | Acredita el monto en la cuenta                                 | -           |
| 5    | Sistema | Genera comprobante con número de transacción único             | -           |

**FLUJO ALTERNO:**

| Paso | Actor   | Descripción                                                    | Excepciones |
|------|---------|----------------------------------------------------------------|-------------|
| 2A   | Sistema | Monto inválido (negativo o cero), retorna error de validación  | -           |
| 3A   | Sistema | Cuenta destino no existe, retorna error 404                    | -           |

| Notas y comentarios: | El depósito se refleja de inmediato en el saldo y queda registrado en el log de transacciones. |
|----------------------|-----------------------------------------------------------------------------------------------|

**ANEXOS**

PROTOTIPOS: Formulario de depósito con campo cuenta destino y monto.

**REGLAS DE NEGOCIO**

| No. | Descripción                                                                 |
|-----|-----------------------------------------------------------------------------|
| 1   | El monto mínimo de depósito es $1.000 COP                                  |
| 2   | El depósito se refleja inmediatamente en el saldo                           |
| 3   | Cada depósito genera un número de transacción único e irrepetible           |

**ABREVIATURAS**

| Abreviatura | Significado                  |
|-------------|------------------------------|
| JWT         | JSON Web Token               |
| COP         | Peso Colombiano              |

**HISTORIAL DE REVISIÓN**

| Elaborado por    | Aprobado por | Fecha      | Descripción y Justificación de Cambios |
|------------------|--------------|------------|----------------------------------------|
| CVDS Company     |              | 22/10/2024 |                                        |
| Nicolás Prieto   |              | 20/06/2026 | Creación del requerimiento RF04        |

---

## Análisis Crítico

### a) ¿Identifica algún requerimiento que deba detallarse más?

RF06 (Enviar reporte a la DIAN en formato JSON) requiere mayor detalle: se deben especificar los campos obligatorios del JSON según la normativa DIAN, la frecuencia de envío, el manejo de errores de rechazo y el proceso de reenvío en caso de fallo.

### b) ¿Existen requerimientos que se contradigan entre sí?

RF05 y RF06 pueden generar tensión: el reporte tributario en PDF para el cliente y el reporte para la DIAN en JSON pueden tener estructuras y periodicidades distintas, lo que implica lógica duplicada si no se diseña un modelo de datos unificado.

### c) ¿Cuáles serían los 2 más importantes para una primera iteración?

1. **RF01 - Autenticación:** Es la base de seguridad del sistema; sin ella ningún otro requerimiento puede operar de forma segura.
2. **RF04 - Depósitos:** Es la operación transaccional más básica y permite validar el núcleo del modelo bancario.

### d) ¿Existe algún requerimiento que NO debería realizarse en el MVP?

RF06 (Enviar reporte a la DIAN en formato JSON) no debería estar en el MVP, ya que depende de integraciones externas con entidades gubernamentales, implica cumplimiento normativo complejo y puede bloquear la entrega del producto central si no se implementa correctamente.

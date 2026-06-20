# Documento de Requerimientos
## Sistema Bancario - DOSW Laboratorio 3

**Equipo:** Hever Barrera, Nicolás Prieto, Mabel Bernal  
**Fecha:** 2026-06-20  
**Versión:** 1.0

---

## 1. Requerimientos Funcionales

| ID  | Descripción |
|-----|-------------|
| RF01 | El sistema debe autenticar usuarios con usuario y contraseña |
| RF02 | El sistema debe registrar y validar cuentas bancarias (10 dígitos, banco registrado) |
| RF03 | El sistema debe permitir consultar el saldo de una cuenta por el cliente |
| RF04 | El sistema debe permitir realizar depósitos a una cuenta |
| RF05 | El sistema debe generar reporte tributario en PDF para el cliente |
| RF06 | El sistema debe enviar reporte a la DIAN en formato JSON |
| RF07 | El sistema debe permitir realizar retiros de una cuenta validando saldo disponible |
| RF08 | El sistema debe permitir transferencias entre cuentas registradas |

---

## 2. Requerimientos No Funcionales

| ID   | Categoría       | Descripción |
|------|-----------------|-------------|
| RNF01 | Seguridad      | Autenticación con tokens JWT |
| RNF02 | Disponibilidad | 99.5% uptime mensual |
| RNF03 | Rendimiento    | Respuesta < 2 segundos por operación |
| RNF04 | Escalabilidad  | Soportar 10.000 usuarios concurrentes |
| RNF05 | Auditabilidad  | Log de todas las transacciones |
| RNF06 | Mantenibilidad | Cobertura de pruebas unitarias mínima del 80% |

---

## 3. Detalle de Requerimientos Seleccionados

### RF01 - Autenticar usuarios con usuario y contraseña

- **Descripción:** El sistema permite a un usuario registrado iniciar sesión proporcionando sus credenciales (usuario y contraseña). Si son válidas, se genera un token JWT.
- **Actores:** Cliente, Sistema
- **Precondiciones:** El usuario debe estar registrado en el sistema.
- **Flujo principal:**
  1. El cliente ingresa usuario y contraseña.
  2. El sistema valida las credenciales contra la base de datos.
  3. El sistema genera y retorna un token JWT.
  4. El cliente accede al sistema.
- **Flujos alternativos:**
  - Si las credenciales son incorrectas, el sistema retorna error 401.
  - Si el usuario está bloqueado, el sistema retorna mensaje de cuenta bloqueada.
- **Postcondiciones:** El cliente tiene un token JWT válido para operar.
- **Criterios de aceptación:**
  - El token JWT expira en 30 minutos.
  - Después de 3 intentos fallidos la cuenta se bloquea temporalmente.

---

### RF03 - Consultar el saldo de una cuenta

- **Descripción:** El cliente autenticado puede consultar el saldo actual de cualquiera de sus cuentas registradas.
- **Actores:** Cliente, Sistema
- **Precondiciones:** El cliente debe estar autenticado con token JWT válido.
- **Flujo principal:**
  1. El cliente selecciona la cuenta a consultar.
  2. El sistema verifica que la cuenta pertenece al cliente.
  3. El sistema retorna el saldo actual y la fecha de última transacción.
- **Flujos alternativos:**
  - Si la cuenta no pertenece al cliente, el sistema retorna error 403.
  - Si la cuenta no existe, el sistema retorna error 404.
- **Postcondiciones:** El cliente visualiza el saldo actualizado.
- **Criterios de aceptación:**
  - El saldo mostrado debe reflejar todas las transacciones en tiempo real.
  - La respuesta debe entregarse en menos de 2 segundos.

---

### RF04 - Realizar depósitos a una cuenta

- **Descripción:** El cliente autenticado puede realizar depósitos de dinero a una cuenta bancaria registrada.
- **Actores:** Cliente, Sistema
- **Precondiciones:** El cliente debe estar autenticado y la cuenta destino debe existir.
- **Flujo principal:**
  1. El cliente selecciona la cuenta destino e ingresa el monto.
  2. El sistema valida que el monto sea mayor a cero.
  3. El sistema acredita el monto en la cuenta.
  4. El sistema genera un comprobante de la transacción.
- **Flujos alternativos:**
  - Si el monto es inválido (negativo o cero), el sistema retorna error de validación.
  - Si la cuenta destino no existe, el sistema retorna error 404.
- **Postcondiciones:** El saldo de la cuenta se incrementa con el monto depositado y se registra en el log de transacciones.
- **Criterios de aceptación:**
  - El depósito se refleja de inmediato en el saldo.
  - Se genera comprobante con número de transacción único.

---

## 4. Análisis Crítico

### a) ¿Identifica algún requerimiento que deba detallarse más?

RF06 (Enviar reporte a la DIAN en formato JSON) requiere mayor detalle: se deben especificar los campos obligatorios del JSON según la normativa DIAN, la frecuencia de envío, el manejo de errores de rechazo y el proceso de reenvío en caso de fallo.

### b) ¿Existen requerimientos que se contradigan entre sí?

RF05 y RF06 pueden generar tensión: el reporte tributario en PDF para el cliente y el reporte para la DIAN en JSON pueden tener estructuras y periodicidades distintas, lo que implica lógica duplicada si no se diseña un modelo de datos unificado.

### c) ¿Cuáles serían los 2 más importantes para una primera iteración?

1. **RF01 - Autenticación:** Es la base de seguridad del sistema; sin ella ningún otro requerimiento puede operar de forma segura.
2. **RF04 - Depósitos:** Es la operación transaccional más básica y permite validar el núcleo del modelo bancario.

### d) ¿Existe algún requerimiento que NO debería realizarse en el MVP?

RF06 (Enviar reporte a la DIAN en formato JSON) no debería estar en el MVP, ya que depende de integraciones externas con entidades gubernamentales, implica cumplimiento normativo complejo y puede bloquear la entrega del producto central si no se implementa correctamente.

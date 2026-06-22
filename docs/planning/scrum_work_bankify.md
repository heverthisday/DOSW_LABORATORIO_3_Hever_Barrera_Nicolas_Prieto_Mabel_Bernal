# Desglose de Trabajo (Scrum) — Bankify

*Épica → Historias de Usuario → Tareas Técnicas*. Nos basamos en los dos requerimientos que elegimos (RF01 y RF04) 

---

## ️ Épica: Login Seguro y Operación Base de Depósitos
* **ID:** `EP-01` | **Jira:** `SCRUM-1`
* **Descripción:** Esta épica. La idea es que el usuario pueda iniciar sesión sin problemas de seguridad y pueda hacer la transacción más básica de todas: meter plata a la cuenta (depósitos). Con esto probamos que la base de datos y la lógica principal funcionen bien antes de ponernos a hacer reportes o consultas.
* **Requerimientos que cubre:** RF01 (Autenticación) y RF04 (Depósitos).
* **Actores:** Cliente.
* **Por qué es importante para el MVP:** Como pusimos en el análisis crítico, sin el login no podemos asegurar nada del sistema y nadie podría entrar. Y los depósitos son la excusa perfecta para testear que la base de datos guarde y sume bien la plata sin errores de código.

---

##  Historias de Usuario (HUs) y Tareas

### HU-01: Login con Usuario y Contraseña (RF01)
* **ID Jira:** `SCRUM-2`
* **Historia:** Como **Cliente de Bankify**,
  quiero **iniciar sesión con mi usuario y clave**,
  para **poder entrar a la aplicación y estar seguro de que nadie más va a ver mi plata**.
* **Prioridad:** Alta
* **Justificación:** Es la precondición de todo el laboratorio. Si no sabemos quién está entrando, las demás pantallas y funciones simplemente no pueden hacer nada, por lo que es obligatoria para arrancar.

####  Criterios de Aceptación
* **Escenario 1 — El usuario mete los datos bien:**
    * **Dado** que el cliente ya tiene una cuenta activa,
    * **Cuando** escribe su usuario y contraseña correctos y le da al botón de "Ingresar",
    * **Entonces** el sistema valida los datos con la base de datos, le suelta su token JWT para mantener la sesión y lo manda al dashboard principal.
* **Escenario 2 — El usuario pone datos mal:**
    * **Dado** que el cliente se equivoca en la clave o el usuario,
    * **Cuando** intenta loguearse,
    * **Entonces** la app le muestra un error genérico (para que no sepa exactamente en qué falló por seguridad) y no lo deja pasar para nada.

####  Tareas Técnicas
1. **T-01.1** `SCRUM-6` Ponerse de acuerdo en cómo se va a conectar el backend y el frontend para el login
2. **T-01.2** `SCRUM-7` Hacer el código del backend que revisa la contraseña y mantiene la sesión activa.
3. **T-01.3** `SCRUM-8` Hacer la pantalla de Login en el frontend con su validación de campos vacíos.

---

###  HU-02: Bloqueo de Cuenta por Errores Seguidos (RF01)
* **ID Jira:** `SCRUM-3`
* **Historia:** Como **Cliente de Bankify**,
  quiero **que la app bloquee mi cuenta si se equivocan muchas veces con la clave**,
  para **evitar que un extraño intente adivinar mi contraseña probando un montón de veces**.
* **Prioridad:**  Media
* **Justificación:** Es un extra de seguridad clave para el login. No frena a un usuario normal que se sabe sus datos, pero nos ayuda a proteger las cuentas de ataques sospechosos.

####  Criterios de Aceptación
* **Escenario 1 — Tres fallos seguidos:**
    * **Dado** que el usuario ya metió la clave mal 2 veces seguidas,
    * **Cuando** se equivoca por tercera vez,
    * **Entonces** el sistema cambia el estado del usuario a "Bloqueado", saca un aviso diciendo cuánto tiempo debe esperar y rechaza cualquier otro intento por ese rato.

####  Tareas Técnicas
1. **T-02.1** `SCRUM-9` Modificar la base de datos para guardar los intentos fallidos y la hora del bloqueo. [Base de Datos]
2. **T-02.2** `SCRUM-10` Crear la lógica que cuente los fallos y controle el tiempo para desbloquear la cuenta. [Backend]
3. **T-02.3** `SCRUM-11` Hacer pruebas automáticas que simulen los 3 fallos para verificar que sí bloquee. [Pruebas]

---

###  HU-03: Hacer Depósitos a la Cuenta (RF04)
* **ID Jira:** `SCRUM-4`
* **Historia:** Como **Cliente autenticado de Bankify**,
  quiero **hacer un depósito poniendo el número de cuenta y el valor**,
  para **ver que el saldo de mi cuenta suba de inmediato**.
* **Prioridad:**  Alta
* **Justificación:** Es la operación más importante del negocio en este punto. Necesitamos asegurar que la app suma bien la plata y guarda los movimientos sin descuadrarse.

####  Criterios de Aceptación
* **Escenario 1 — Depósito exitoso:**
    * **Dado** que la cuenta a la que se le va a meter la plata sí existe y está activa,
    * **Cuando** el usuario digita un valor válido (mayor al mínimo de $1.000 COP) y confirma,
    * **Entonces** el sistema actualiza el saldo en la base de datos en una sola operación y le muestra un código de comprobante único en pantalla.

####  Tareas Técnicas
1. **T-03.1** `SCRUM-12` Estructurar qué datos va a recibir y responder la ruta de depósitos. [Backend]
2. **T-03.2** `SCRUM-13` Crear el código para registrar el depósito de forma segura y actualizar el saldo en la BD. [Backend]
3. **T-03.3** `SCRUM-14` Hacer el formulario de depósitos en el frontend y validar que no metan letras o dejen campos vacíos. [Frontend]

---

###  HU-04: Validar Monto Mínimo del Depósito (RF04)
* **ID Jira:** `SCRUM-5`
* **Historia:** Como **Cliente autenticado de Bankify**,
  quiero **que la app me rebote el depósito si pongo valores que no tienen sentido**,
  para **evitar meter mal el dedo o hacer transacciones por error**.
* **Prioridad:**  Baja
* **Justificación:** Esto es más que todo control de errores y pulir la interfaz. La lógica fuerte de mover plata ya se hace en la HU-03, esto es para que el usuario no meta datos inválidos por accidente.

####  Criterios de Aceptación
* **Escenario 1 — Intentar depositar plata inválida:**
    * **Dado** que el cliente está en la pantalla de depósitos,
    * **Cuando** intenta mandar un monto en cero, negativo, o menor a $1.000 COP,
    * **Entonces** la app frena el envío de una, saca un letrero rojo explicando las reglas de montos mínimos y no manda nada al backend.

####  Tareas Técnicas
1. **T-04.1** `SCRUM-15` Hacer una validación en el servicio del backend para que enlance una excepción personalizada si el monto es menor al mínimo de la app ($1.000 COP). [Backend]
2. **T-04.2** `SCRUM-16` Diseñar los avisos o alertas en el Frontend para mostrar el mensaje de error exacto que responda la API. [Frontend]
3. **T-04.3** `SCRUM-17` Realizar pruebas funcionales de validación de montos. [Pruebas]


---


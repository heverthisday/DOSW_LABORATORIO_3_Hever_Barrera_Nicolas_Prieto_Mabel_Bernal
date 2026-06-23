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
* **Estimación (Planning Poker):** `8 puntos`
* **Justificación de estimación:** Involucra tres capas con dependencias: backend con JWT, frontend con formulario y validación, y BD para verificar credenciales. El riesgo técnico es alto porque es la base de seguridad de todo el sistema.
* **Justificación:** Es la precondición de todo el laboratorio. Si no sabemos quién está entrando, las demás pantallas y funciones simplemente no pueden hacer nada, por lo que es obligatoria para arrancar.
* **Video Planning Poker:** [https://pruebacorreoescuelaingeduco.sharepoint.com/:v:/s/samuelesgay/IQD0HIl9ixjzRJRX_Q87PeLIASzuXijohnC9Ycziy4EY9PY?e=3glq5P&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D]


###  HU-02: Bloqueo de Cuenta por Errores Seguidos (RF01)
* **ID Jira:** `SCRUM-3`
* **Historia:** Como **Cliente de Bankify**,
  quiero **que la app bloquee mi cuenta si se equivocan muchas veces con la clave**,
  para **evitar que un extraño intente adivinar mi contraseña probando un montón de veces**.
* **Prioridad:**  Media
* **Estimación (Planning Poker):** `5 puntos`
* **Justificación de estimación:** Depende de HU-01 ya hecha. La lógica es más acotada — conteo de intentos fallidos y control de tiempo de bloqueo — pero requiere cambios en BD y pruebas específicas. No tiene pantalla nueva en el frontend.
* **Justificación:** Es un extra de seguridad clave para el login. No frena a un usuario normal que se sabe sus datos, pero nos ayuda a proteger las cuentas de ataques sospechosos.



###  HU-03: Hacer Depósitos a la Cuenta (RF04)
* **ID Jira:** `SCRUM-4`
* **Historia:** Como **Cliente autenticado de Bankify**,
  quiero **hacer un depósito poniendo el número de cuenta y el valor**,
  para **ver que el saldo de mi cuenta suba de inmediato**.
* **Prioridad:**  Alta
* **Estimación (Planning Poker):** `8 puntos`
* **Justificación de estimación:** Operación transaccional en BD, generación de comprobante único y actualización de saldo en tiempo real. Alto riesgo técnico porque un error aquí afecta directamente la integridad del dinero. Requiere coordinación entre backend y frontend.
* **Justificación:** Es la operación más importante del negocio en este punto. Necesitamos asegurar que la app suma bien la plata y guarda los movimientos sin descuadrarse.




---

###  HU-04: Validar Monto Mínimo del Depósito (RF04)
* **ID Jira:** `SCRUM-5`
* **Historia:** Como **Cliente autenticado de Bankify**,
  quiero **que la app me rebote el depósito si pongo valores que no tienen sentido**,
  para **evitar meter mal el dedo o hacer transacciones por error**.
* **Prioridad:**  Baja
* **Estimación (Planning Poker):** `3 puntos`
* **Justificación de estimación:** Es control de errores sobre HU-03 ya definida. Solo requiere una validación en el servicio backend con excepción personalizada y el mensaje de error en el frontend. Sin lógica de negocio nueva ni cambios en BD.
* **Justificación:** Esto es más que todo control de errores y pulir la interfaz. La lógica fuerte de mover plata ya se hace en la HU-03, esto es para que el usuario no meta datos inválidos por accidente.





---
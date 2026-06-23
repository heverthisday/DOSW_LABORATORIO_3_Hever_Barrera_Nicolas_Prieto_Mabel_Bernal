# DOSW Laboratorio 3 — Bankify

## Equipo
- Hever Barrera
- Nicolás Prieto
- Mabel Bernal

## Objetivo del Laboratorio
Aprender a definir y analizar requerimientos de software a partir de un caso de estudio real (Bankify), y aplicar el framework Agile Scrum usando Jira para planear el trabajo de desarrollo. El lab cubre las tres primeras fases del ciclo de vida del software: definición, análisis y planeación.

**Workspace Jira:** https://teamdosw.atlassian.net

---

## Preguntas Teóricas

### 1. ¿Qué es un pull request en GitHub?

Un pull request (o PR) es básicamente una forma de pedirle al equipo que revise los cambios que hiciste en una rama antes de mezclarlos con la rama principal. Es como decir "oye, hice estos cambios, ¿alguien los revisa y me da el visto bueno?". Sirve para que no llegue código roto o sin revisar a la rama principal, y también queda un historial de quién aprobó qué.

### 2. ¿Cómo se crea un pull request en GitHub?

Primero tienes que tener tus cambios subidos en una rama distinta a main o develop. Luego entras al repositorio en GitHub, vas a la pestaña **Pull requests** y le das a **New pull request**. Ahí seleccionas la rama de origen (la tuya con los cambios) y la rama destino (por ejemplo develop), le pones un título y una descripción explicando qué hiciste, y das clic en **Create pull request**. Después le avisas a un compañero para que lo revise.

### 3. ¿Cómo se aprueba un pull request en GitHub?

El compañero que va a revisar entra al PR, ve los cambios en la pestaña **Files changed** y puede dejar comentarios en líneas específicas si algo no le cuadra. Si todo está bien, va a **Review changes**, selecciona **Approve** y envía la revisión. Una vez aprobado, quien tenga permisos puede darle a **Merge pull request** para mezclar los cambios con la rama destino. Después de hacer el merge se borra la rama para mantener el repo limpio.

### 4. Bibliografía en norma APA

GitHub. (2024). *About pull requests*. GitHub Docs. https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests

GitHub. (2024). *Creating a pull request*. GitHub Docs. https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request

GitHub. (2024). *Approving a pull request with required reviews*. GitHub Docs. https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/approving-a-pull-request-with-required-reviews

---

## Reflexión — Planning Poker 

### ¿Cuál fue la mayor dificultad a la hora de estimar?

La mayor dificultad fue ponernos de acuerdo en HU-01 y HU-03, que las dos nos salieron en 8 puntos. El problema fue que cada uno le daba un peso distinto al riesgo técnico: unos miraban cuántas horas podría tomarse la tarea, otros miraban qué tan difícil era la lógica y cuántas cosas podían salir mal. Al final tuvimos que separar la conversación entre complejidad técnica e incertidumbre para llegar a un número que nos convenciera a todos.

### ¿Fue fácil llegar a un consenso?

Para HU-02 y HU-04 fue bastante rápido porque la lógica era más acotada y los tres teníamos una idea similar de lo que había que hacer. Donde más nos costó fue en HU-01, porque alguien la veía como un 5 argumentando que el login es algo estándar, y otros la veíamos como un 13 por la parte de seguridad con JWT. Después de que cada uno explicó su razonamiento llegamos al 8 como punto medio justificado.

### ¿Cómo resolvieron las discrepancias grandes?

Cuando había diferencia grande entre votos, el que puso el número más alto y el que puso el más bajo explicaban su razonamiento. Casi siempre la discrepancia venía de que uno estaba pensando solo en el backend y el otro estaba incluyendo también el frontend y las pruebas. Una vez que pusimos en la mesa qué tareas incluía cada historia, fue más fácil llegar a un acuerdo sin que nadie tuviera que ceder a la fuerza.

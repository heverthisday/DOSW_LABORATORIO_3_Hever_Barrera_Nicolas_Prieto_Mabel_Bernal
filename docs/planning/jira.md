# Jira - Product Backlog
## Sistema Bancario Bankify - DOSW Laboratorio 3
**Equipo:** Hever Barrera, Nicolás Prieto, Mabel Bernal
**Proyecto Jira:** https://teamdosw.atlassian.net
---
## 1. Épica
| Campo       | Detalle                                      |
|-------------|----------------------------------------------|
| ID          | SCRUM-1                                      |
| Título      | Login Seguro y Operación Base de Depósitos   |
| Link        | https://teamdosw.atlassian.net/browse/SCRUM-1 |

![Épica Jira](../images/jiraEpica.png)
[Ver épica en Jira](https://teamdosw.atlassian.net/browse/SCRUM-1)
---
## 2. Historias de Usuario
### SCRUM-2 - Login con usuario y contraseña
![Historia 1](../images/JiraHistoria1.png)
[Ver historia en Jira](https://teamdosw.atlassian.net/browse/SCRUM-2)
---
### SCRUM-3 - Bloqueo de cuenta por errores seguidos
![Historia 2](../images/JiraHistoria2.png)
[Ver historia en Jira](https://teamdosw.atlassian.net/browse/SCRUM-3)
---
### SCRUM-4 - Realizar depósitos en una cuenta bancaria
![Historia 3](../images/JiraHistoria3.png)
[Ver historia en Jira](https://teamdosw.atlassian.net/browse/SCRUM-4)
---
### SCRUM-5 - Validar monto mínimo de depósito
![Historia 4](../images/JiraHistoria4.png)
[Ver historia en Jira](https://teamdosw.atlassian.net/browse/SCRUM-5)
---
## 3. Tareas
### SCRUM-6 - Definir integración frontend-backend para login
![Tarea 1](../images/JiraTarea1.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-6)
---
### SCRUM-7 - Implementar autenticación y gestión de sesión
![Tarea 2](../images/JiraTarea2.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-7)
---
### SCRUM-8 - Desarrollar pantalla de login y validaciones
![Tarea 3](../images/JiraTarea3.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-8)
---
### SCRUM-9 - Agregar campos de intentos fallidos en la base de datos
![Tarea 4](../images/JiraTarea4.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-9)
---
### SCRUM-10 - Implementar lógica de bloqueo y desbloqueo
![Tarea 5](../images/JiraTarea5.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-10)
---
### SCRUM-11 - Crear pruebas automáticas para bloqueo
![Tarea 6](../images/JiraTarea6.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-11)
---
### SCRUM-12 - Diseñar endpoint de depósitos
![Tarea 7](../images/JiraTarea7.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-12)
---
### SCRUM-13 - Implementar actualización de saldo y registro de depósito
![Tarea 8](../images/JiraTarea8.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-13)
---
### SCRUM-14 - Desarrollar formulario de depósitos
![Tarea 9](../images/JiraTarea9.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-14)
---
### SCRUM-15 - Implementar validación de monto mínimo
![Tarea 10](../images/JiraTarea10.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-15)
---
### SCRUM-16 - Diseñar mensajes de error para depósitos inválidos
![Tarea 11](../images/JiraTarea11.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-16)
---
### SCRUM-17 - Realizar pruebas funcionales de validación de montos
![Tarea 12](../images/JiraTarea12.png)
[Ver tarea en Jira](https://teamdosw.atlassian.net/browse/SCRUM-17)
---
## 4. Timeline
![Timeline Jira](../images/JiraTime.png)

---

## 5. Sprint Backlog

### Historias incluidas en el Sprint 1

| Historia | Puntos | Prioridad | Justificación de inclusión |
|----------|--------|-----------|---------------------------|
| HU-01: Login con Usuario y Contraseña | 8 | Alta | Precondición de todo el sistema |
| HU-03: Hacer Depósitos a la Cuenta | 8 | Alta | Operación core del negocio |
| **Total** | **16 puntos** | | |

### Historias excluidas del Sprint 1

| Historia | Puntos | Prioridad | Justificación de exclusión |
|----------|--------|-----------|---------------------------|
| HU-02: Bloqueo de Cuenta por Errores Seguidos | 5 | Media | Depende de HU-01. Se incluye en Sprint 2 una vez el login base esté estable |
| HU-04: Validar Monto Mínimo del Depósito | 3 | Baja | Depende de HU-03. Es refinamiento de la funcionalidad, no el core |

### Asignación de Responsables por Tarea

#### HU-01: Login con Usuario y Contraseña

| Tarea | Descripción | Responsable |
|-------|-------------|-------------|
| T-01.1 `SCRUM-6` | Definir integración frontend-backend para login | Hever Barrera |
| T-01.2 `SCRUM-7` | Implementar autenticación y gestión de sesión | Nicolás Prieto |
| T-01.3 `SCRUM-8` | Desarrollar pantalla de login y validaciones | Mabel Bernal |

#### HU-03: Hacer Depósitos a la Cuenta

| Tarea | Descripción | Responsable |
|-------|-------------|-------------|
| T-03.1 `SCRUM-12` | Diseñar endpoint de depósitos | Nicolás Prieto |
| T-03.2 `SCRUM-13` | Implementar actualización de saldo y registro de depósito | Hever Barrera |
| T-03.3 `SCRUM-14` | Desarrollar formulario de depósitos | Mabel Bernal |

### Justificación de la Decisión de Planeación

Se eligieron HU-01 y HU-03 para el Sprint 1 por dos razones principales.

Primero, son las dos historias de prioridad Alta según el análisis crítico del equipo. Sin el login no existe forma de saber quién está usando el sistema, lo que hace inviable cualquier otra funcionalidad. Y los depósitos son la operación de negocio más básica de Bankify — si eso no funciona bien, el MVP no tiene sentido.

Segundo, siguiendo el criterio del lab (prioridad Alta primero, luego menor estimación de puntos), HU-02 y HU-04 quedan por fuera porque además de tener menor prioridad, dependen de que HU-01 y HU-03 estén terminadas respectivamente. Meterlas en el mismo sprint generaría bloqueos innecesarios entre tareas.

Con 16 puntos en el Sprint 1 el equipo tiene una carga manejable que permite entregar valor real al finalizar la iteración: un usuario puede entrar al sistema y hacer un depósito, que es exactamente lo que Bankify necesita validar en su MVP.

### Captura Sprint Backlog en Jira

<img width="2559" height="914" alt="image" src="https://github.com/user-attachments/assets/7b50b468-c36b-4202-819b-ebdf2bc92e2d" />

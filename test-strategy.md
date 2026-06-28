# 🎯 Estrategia de Pruebas y Plan de Ataque - QA Banrural

Este documento describe el enfoque estratégico utilizado para auditar, detectar errores e implementar mejoras de calidad en el aplicativo **Juego Adivina tu Número**.

---

## 1. Alcance de las Pruebas (Scope)
El análisis se enfocó en garantizar la correcta implementación de las reglas de negocio, la integridad de los datos de entrada y la consistencia de la experiencia del usuario (UX) mediante pruebas estáticas del código fuente y dinámicas en el navegador.

### Reglas de Negocio Validadas:
* Generación correcta de números enteros en el rango cerrado `[1, 100]`.
* Límite estricto e inquebrantable de 10 intentos máximos por sesión.
* Manejo adecuado del estado físico y lógico de los controles durante y después del juego.

---

## 2. Tipos de Pruebas Ejecutadas

### A. Pruebas Funcionales (Caja Negra)
* **Flujo Feliz:** Verificación del comportamiento del sistema cuando el usuario adivina el número secreto.
* **Flujos Alternos:** Verificación del comportamiento al fallar consecutivamente hasta alcanzar el límite de 10 turnos.
* **Pruebas de Frontera / Valores Límite:** Ingreso manual de valores mínimos (`1`), máximos (`100`), e inmediatamente fuera del límite (`0`, `101`, `-5`).

### B. Pruebas de Interfaz (UI) y UX
* Validación de contrastes y legibilidad del texto en estados cambiantes.
* Coherencia de colores de alerta según estándares convencionales (Verde = Éxito / Rojo = Error).

---

## 3. Matriz de Defectos Corregidos (Bug Log)

| ID | Componente | Descripción del Defecto | Severidad | Prioridad | Resolución / Acción Correctiva |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **BUG-001** | Interfaz (UI) | El fondo de la alerta de error "¡Incorrecto!" se mostraba verde, contradiciendo el mensaje. | Media | Alta | Se modificó el estilo a color `red` para ser visualmente coherente con una falla. |
| **BUG-002** | Estilos (CSS) | Al reiniciar la partida el fondo cambiaba a blanco, causando que las letras blancas (`color: white`) fueran invisibles. | Alta | Alta | Se cambió el reinicio del color de fondo a `transparent`, manteniendo legibilidad total. |
| **BUG-003** | Lógica / Datos | Campos vacíos o texto se procesaban como el número `0`, restando intentos válidos de manera injusta al jugador. | Alta | Alta | Se implementó una cláusula de guarda en JavaScript para evitar el envío de nulos, strings o rangos fuera de 1-100 sin consumir turnos. |

---

## 4. Casos de Prueba Clave Automatizables / Manuales

### TC-001: Validación de Datos Inválidos
* **Entrada:** Input vacío (`""`) o cadena de texto (`"BanruralQA"`).
* **Acción:** Presionar el botón de envío.
* **Resultado Esperado:** Despliegue de alerta nativa sin agregar datos a la lista de "Números anteriores" y manteniendo el contador de intentos intacto.

### TC-002: Ciclo de Vida de Reinicio
* **Entrada:** Hacer clic en "Comienza un nuevo juego" tras haber ganado o perdido.
* **Acción:** Ejecutar una jugada errónea en la segunda ronda.
* **Resultado Esperado:** El texto "¡Incorrecto!" debe ser 100% legible, los campos de historial vacíos y los botones completamente habilitados.

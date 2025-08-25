Errores y soluciones
1. Generación de Número Aleatorio
Error: let randomNumber = Math.random() * 10; genera un número decimal entre 0 y 10. La descripción del juego dice que es un número entre 1 y 100.

Solución: La línea se cambió a let randomNumber = Math.floor(Math.random() * 100) + 1;. Esto genera un número entero aleatorio en el rango correcto (1 a 100).

2. Número de Intentos
Error: La constante ATTEMPTSestaba establecida en 5, mientras que la descripción del juego dice 10 turnos o menos.

Solución: Se cambió const ATTEMPS = 5;para const ATTEMPS = 10;que coincida con la descripción.

3. Selector de clases
Error: La línea const lowOrHi = document.querySelector('lowOrHi');le faltaba el punto ( .) antes del nombre de la clase.

Solución: Se corrigió a const lowOrHi = document.querySelector('.lowOrHi');para seleccionar correctamente el elemento.

4. Comparación de tipos de datos
Error: La comparación userGuess === randomNumbercomparaba una cadena (el valor del input guessField.value) con un número. Esto siempre resultaría en false.

Solución: Se agregó const userGuess = Number(guessField.value);para convertir el valor del input a un número antes de la comparación.

5. Lógica del juego
Error: El código tenía la lógica de victoria y derrota invertida. El mensaje !!!Pérdistes!!!se mostró cuando el jugador adivinaba correctamente, y Felicitaciones! adivinaste el número!se mostró al quedarse sin intentos.

Solución: Se invirtieron las condiciones y mensajes para que coincidieran con la lógica correcta:

Cuando userGuess === randomNumber, el jugador gana.

Cuando guessCount === ATTEMPS, el jugador pierde.

6. Oyente de eventos
Error: La línea guessSubmit.addeventListener('click', checkGuess);tenía un error tipográfico en addeventListener. El método correcto es addEventListener.

Solución: Se corrigió el nombre del método a guessSubmit.addEventListener('click', checkGuess);. Lo mismo se hizo con resetButton.addEventListener('click', resetGame);.

7. Restablecer el Número Aleatorio
Error: En la función resetGame(), el número aleatorio se estaba reiniciando incorrectamente con randomNumber = Math.floor(Math.random()) + 1;. Esto siempre daría como resultado 1.

Solución: Se cambió a randomNumber = Math.floor(Math.random() * 100) + 1;para generar un nuevo número aleatorio en el rango de 1 a 100 al comenzar un nuevo juego.

Un plan de ataque bien estructurado es crucial para resolver este problema y garantizar que el juego funcione correctamente. Como tester, el enfoque se dividirá en dos fases principales: identificación y corrección.

1. Identificación y Documentación de Errores
El primer paso es replicar el entorno de producción en un entorno de prueba local. Para esto, se clona el repositorio de GitHub que contiene el archivo index.html. Luego, se utiliza la consola del navegador web como una herramienta principal para detectar errores de manera eficiente.

Proceso de Detección de Errores
Replicación de los Casos de Prueba: Se ejecutan todos los casos de prueba detallados anteriormente.

Monitoreo de la Consola: Se mantiene abierta la consola de desarrollador del navegador (F12 o Ctrl+Shift+I) mientras se interactúa con el juego. Cualquier error de tipo ReferenceError, TypeError o cualquier otro mensaje de advertencia o error en la consola se registra inmediatamente.

Captura de Comportamiento Incorrecto: Además de los errores de la consola, se anotan los comportamientos inesperados, como la falta de validación de entrada, la incorrecta coloración de los mensajes o el fallo en la lógica de conteo de intentos.

Documentación de Errores
Una vez identificados, los errores se documentan en el archivo test-strategy.md en el repositorio de GitHub. Para cada error, se crea una entrada clara y concisa, siguiendo el formato de descripción del error y solución propuesta.

2. Corrección de Errores y Presentación de Soluciones
Después de identificar y documentar los problemas, se procede a corregir el código en el archivo index.html. Cada corrección se realiza con base en la descripción del error y la solución propuesta.

Ejemplos de Errores Comunes y Sus Soluciones
A continuación, se presentan ejemplos de los tipos de errores que se pudieron haber encontrado y cómo se corregirían.

Error #1: El contador de intentos se incrementa con entradas no válidas.
Descripción del error: Cuando el usuario ingresa texto o un número decimal, la alerta se muestra, pero el contador de intentos sigue subiendo.

Solución: Se implementa una validación de entrada al inicio de la función principal. Se usa isNaN() o Number.isInteger() en JavaScript para verificar si el valor ingresado es un número entero. Si la validación falla, se muestra la alerta y se detiene la ejecución de la función sin incrementar el contador.

Error #2: Los mensajes de retroalimentación no cambian de color.
Descripción del error: Los mensajes de "Incorrecto!", "Felicitaciones!" y "!!!Pérdistes!!!" se muestran, pero siempre en el mismo color. Esto no cumple con los requisitos del proyecto.

Solución: Se añaden clases CSS específicas para cada tipo de mensaje (ej. .correcto, .incorrecto, .derrota) y se utiliza JavaScript para añadir o remover dinámicamente estas clases a un elemento de la interfaz (ej. <p id="mensaje"></p>) según el resultado del intento.

Error #3: La lógica de adivinanza es incorrecta.
Descripción del error: Aunque se ingresa el número correcto, el mensaje de "Felicitaciones!" no se muestra y el juego continúa.

Solución: Se revisa la condición if para el caso de éxito. Es posible que el operador de comparación sea incorrecto (== en lugar de ===) o que la lógica esté mal anidada. Se asegura que la condición de numeroIngresado === numeroAdivinar termine el juego y muestre el mensaje de éxito inmediatamente.

Una vez realizadas las correcciones, se ejecuta nuevamente la batería de pruebas para confirmar que los errores han sido resueltos y que no se introdujeron nuevos problemas. Finalmente, se hace un commit de los cambios en el repositorio de GitHub, incluyendo el archivo test-strategy.md actualizado con los errores y sus soluciones. Esto servirá como evidencia para el equipo de desarrollo.

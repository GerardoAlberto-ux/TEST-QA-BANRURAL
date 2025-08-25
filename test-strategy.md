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

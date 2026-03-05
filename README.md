# Ejercicio en Clase 3 – Modularización en Java
## Curso: Programación 1

## Parte 1 – Análisis del Programa Original

### 1️ Identificación de Tareas Repetitivas

Cuando vi el programa original, me di cuenta que todo estaba metido en el main y eso hacía difícil entenderlo. Identifiqué varias cosas que se podían separar:

- Agregar estudiante
- Mostrar la lista
- Calcular el promedio
- Encontrar al estudiante con mejor nota
- Mostrar el menú

Estas tareas estaban todas revueltas en el main, entonces si quería cambiar algo había que buscar entre mucho código.

Separarlas en métodos me pareció buena idea porque:
- El código queda más ordenado y se entiende mejor
- Si hay un error, solo reviso un método, no todo el programa
- Cada método hace una cosa específica y ya
  

### 2️ Variables Locales vs Globales

En el programa usé variables globales y locales.

**Las globales (static) que dejé:**
- `estudiantes` y `calificaciones` - porque casi todos los métodos las ocupan
- `scanner` - para no estar creando uno nuevo cada rato

**Las locales que creé:**
- `nombre` y `calificacion` - solo cuando agrego estudiante
- `suma` y `promedio` - solo para calcular el promedio
- `maxCalificacion` y `estudianteMax` - solo para buscar al mejor

Creo que es mejor tener las variables solo donde se necesitan. Si `suma` fuera global, podría guardar valores de operaciones anteriores y causar errores. Así, cada vez que llamo al método, empieza desde cero.


## Parte 2 – Modularización del Programa

Reorganicé el código creando métodos para cada tarea:

- `mostrarMenu()` - muestra las opciones
- `leerOpcion()` - lee lo que elige el usuario
- `agregarEstudiante()` - pide nombre y nota, y los guarda
- `mostrarEstudiantes()` - muestra todos los estudiantes
- `calcularPromedio()` - calcula el promedio de notas
- `mostrarMejorEstudiante()` - busca la nota más alta

Cada método hace una sola cosa. Por ejemplo, `mostrarMenu()` solo muestra el menú y no hace nada más. El main ahora solo llama a los métodos según la opción que elija el usuario.

Al principio me confundí un poco con qué parámetros pasarle a cada método, pero al final opté por usar variables globales para las listas porque así todos los métodos pueden verlas sin complicarme tanto.


## Parte 3 – Validaciones y Manejo de Excepciones

Cuando probé el programa original, me pasaba que si escribía una letra en lugar de número, el programa explotaba (tiraba error y se cerraba). Tocaba mejorarlo.

**Qué errores encontré:**
- Si el usuario escribe letras en la opción del menú
- Si escribe letras en la calificación
- Si deja el nombre vacío
- Si pone calificaciones negativas o mayores a 100 (no tenía sentido)

**Qué validaciones hice:**
- Usé `try-catch` para atrapar cuando el usuario no escribe números
- Con `trim()` quité espacios y verifiqué que el nombre no esté vacío
- Agregué un `if` para que la nota esté entre 0 y 100
- Si algo falla, muestro mensaje de error pero el programa sigue

**Por qué son importantes:**
La verdad es que un programa que se cae cuando el usuario se equivoca da mala imagen. Con estas validaciones, aunque el usuario escriba cualquier cosa, el programa responde con un mensaje y sigue funcionando. Además, los datos quedan más limpios para hacer cálculos después.


## Parte 4 – Preguntas de Reflexión

### 1️ ¿Qué ventajas tiene dividir el código en métodos?
Pues la principal es que el código se entiende mejor. También es más fácil encontrar errores porque cada método es pequeño. Otra cosa es que si después quiero agregar más funcionalidades, ya tengo una base ordenada.

### 2️ ¿Por qué no es recomendable usar muchas variables globales?
Porque cualquier método las puede cambiar sin que me dé cuenta. Si tengo muchas globales, es fácil que un método modifique algo que no debería y cause errores difíciles de encontrar. Mejor tenerlas locales a menos que sea necesario compartirlas.

### 3️ ¿Cómo mejora la modularización la legibilidad del código?
Mejora bastante porque en lugar de leer 100 líneas seguidas, veo métodos con nombres que dicen lo que hacen. Por ejemplo, si veo `calcularPromedio()`, ya sé qué hace sin necesidad de leer el código de adentro.


## Conclusión

El programa original funcionaba, pero era difícil de leer y mantener. Con los cambios que hice:
- Separé en métodos
- Usé bien las variables globales y locales
- Agregué validaciones para evitar errores
- Implementé try-catch para que no se caiga

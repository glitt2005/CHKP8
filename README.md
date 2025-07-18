# 1.  ¿Qué tipo de bucles hay en JS?

Una de las formas más comunes de utilizar bucles o **loops** en JS es en colecciones de datos. Examinamos los diferentes tipos de bucles.

### 1) Bucle `for`:

El bucle **for** es el más clásico, y constituye **uno de los más antiguos y versátiles** en JavaScript. Es ideal cuando necesitas un control preciso **sobre el índice en cada iteración** o necesitas **manipular la secuencia** de iteración.

**SINTAXIS**

```javascript
for (inicialización; condición; actualización) { // código a ejecutar }
```

**EJEMPLO: Imprimimos los días de la semana**

```javascript
var diasDeLaSemana = [
    "lunes",
    "martes",
    "miercoles",
    "jueves",
    "viernes",
    "sábado",
    "domingo"
];
    
for (diaSemana = 0; diaSemana < diasDeLaSemana.length; diaSemana++) {
    console.log(diasDeLaSemana[diaSemana]);
}
```

NECESITAMOS:

1. una **variable iteradora**. Aquí es `diaSemana` será utilizada a lo largo del bucle y recorrerá cada elemento del array `diasDeLaSemana`. Pero ojo! esta **variable iteradora** no representa un valor, sino un **índice**!
2. declarar **una condición**, es decir lo que queremos que se cumpla en el bucle. El bucle se parará cuando está condición ya no se cumpla. En nuestro caso, la condición es que sea menor que menor que 7.
   * **Ojo!** ponemos **`< 7` (o sea, hasta 6 inclusive**) en lugar de **`<=7`** porque recordemos que los **índices comienzan en 0** (no en 1). Por lo tanto siempre va a restar 1 del número total de los elementos del array.
   * Otra opción es poner un **-1 al final**, y funcionaría: **sería cuestión de gustos** en cuánto a qué te parece más fácil de leer.

```javascript
for (diaSemana = 0; diaSemana <= (diasDeLaSemana.length -1); diaSemana++) {
    console.log(diasDeLaSemana[diaSemana]);
}
```

3. un tipo de **incrementador**: **var++**, que aumentará en 1, cada vez que haga el bucle.

**VENTAJAS**

• **Control total sobre el índice**: Puedes **acceder y manipular el índice** en cada iteración. • **Flexibilidad**: Permite **saltar o repetir elementos** modificando el índice según sea necesario. • **Compatibilidad amplia**: Funciona en **todas las versiones de JavaScript** y es ideal para estructuras de datos complejas como matrices bidimensionales.

**LIMITACIONES**

• **Propenso a errores**: Es fácil **olvidar incrementar el índice** o establecer incorrectamente las condiciones del bucle. • **Código más verboso**: Requiere **más líneas de código** en comparación con otras

### 2) Bucle `for - in`:

El bucle **for-in** es más moderno que el anterior y tiene un **lectura más sencilla y moderna** para recorrer arrays. Generalmente se utiliza más que el bucle **for**.

* **Sin condiciones**
* **Sin incrementadores**
* El bucle **for-in** interpreta que **debe iterar tantas veces como elementos** estén contenidos en la colección

**SINTAXIS**

```javascript
for (variable in objecto)
  declaración
```

**CONVENCIÓN SINTÁCTICA**: Para el nombre de la **variable iteradora**, usamos el **nombre de la lista** pero **en singular.** En el ejemplo siguiente, pondremos un nombre de array algo más largo (`diasDeLaSemana` ) para que se vea rápidamente la diferencia entre los dos.

#### a) Bucle `for - in` en arrays:

**EJEMPLO: Imprimimos los días de la semana**

```javascript
var diasDeLaSemana = [
    "lunes",
    "martes",
    "miercoles",
    "jueves",
    "viernes",
    "sábado",
    "domingo"
];
    
for (diaSemana in diasDeLaSemana) {
    console.log(diasDeLaSemana[diaSemana]);
}
```

Como vemos la sintaxis es más **sencilla y corta** que la anterior.

#### b) Bucle `for - in` en objetos:

* Esto **muy común cuando llamamos a una API,** es decir, salimos a otro servidor (por ejemplo, _**Twitter**_) y extraemos _tweets_. Éstos son **con frecuencia enviados en formato objeto**, es decir con una estructura de pares clave:valor.
* **Si queremos mostrar esos datos en una página**, la forma de hacerlo es **iterando** sobre esos datos, ese objeto. Y una de las formas más comunes de hacerlo es mediante este bucle **for - in**.

**EJEMPLO: Imprimimos características de un coche**

```javascript
const coche = {
  marca: "Toyota",
  modelo: "Auris",
  año: 2013,
  color: "Rojo"
};

for (let propiedad in coche) {
  console.log("La propiedad " + propiedad + " tiene el valor: " + coche[propiedad]);
}

/* Imprime:
La propiedad marca tiene el valor: Toyota
La propiedad modelo tiene el valor: Auris
La propiedad año tiene el valor: 2013
La propiedad color tiene el valor: Rojo
*/
```

**NOTAS:**

1. `propiedad`es el **elemento iterador**, que representa a la **clave** del par **clave:valor** de cada objeto.
2. Precisamente como se trata de un objeto, **para extraer el `valor`de objeto** necesitaremos utilizar la sintaxis adecuada, que son los **corchetes \[ ].**

**No funcionaría** si utilizáramos la _**dot notation**_ o anotación con puntos para objetos (nos devolvería `underfined` ). Ciertamente éste último sistema de **anotación por puntos** es considerado **una buena práctica**, **pero** en ciertos casos, como en éste, donde la misma **variable iteradora corresponde también a la clave** del par clave:valor **del objeto**, necesitamos ser **más específicos** y utilizar **la sintaxis de corchetes \[ ].**

### 3) Bucle `forEach()`

El método `forEach()` es un **método específico para arrays** que ejecuta una función proporcionada una vez por cada elemento del array.

**SINTAXIS**

```javascript
array.forEach(function() {
    // código
});
```

\
NECESITAMOS:

* **Elemento iterador**: nombre de la variable que representa cada elemento a iterar.
* **Colección**: sobre la que se van a iterar los elementos
* **Instrucciones a ejecutar**. La función dentro de una función se llama función **callback**. Técnicamente no es una función normal, ya que esto sucede automáticamente.

**EJEMPLO: Imprimimos los días de la semana**

```javascript
var diasDeLaSemana = [
    "lunes",
    "martes",
    "miercoles",
    "jueves",
    "viernes",
    "sábado",
    "domingo"
];
    
diasDeLaSemana.forEach(function(diaSemana){
    console.log(diaSemana);
})
```

**VENTAJAS**

• Es relativamente nuevo; **el más moderno, funcional y sencillo** en Javascript. • **Sintaxis concisa:** Más fácil de leer y escribir, especialmente con funciones flecha. • **Evita errores de índice**: No necesitas preocuparte por manejar el índice manualmente. • **Ideal para operaciones en cada elemento**: Perfecto para aplicar una operación a cada elemento.

**LIMITACIONES**

• **No permite break o continue**: No puedes interrumpir o saltar iteraciones dentro del bucle. • **Solo para arrays:** No funciona directamente con otros iterables como cadenas o conjuntos. • **Asincronía limitada:** `forEach ()`**no es ideal para** manejar funciones asíncronas con **`async` - `await`,** ya que no esperará a que cada operación termine.

### 4) Bucle `while` :

**SINTAXIS**

```javascript
while (condition) {
  // código
  // llamado "cuerpo del bucle"
}
```

Mientras la condición `condition` sea verdadera, el `código` del cuerpo del bucle será ejecutado.\
NECESITAMOS:

* **una variable iteradora** y la declaramos **fuera del ámbito de bucle.** Esto puede tener sus puntos negativos **en caso de que no quieras que se tenga acceso a esta variable exterior** más tarde.
* para evitar **un bucle infinito**, necesitamos **el incrementador** a fin de que haga cambiar el valor de la variable iterativa. Añadimos este elemento manualmente dentro del código a ejecutar, **dentro de las llaves{}.**

\


**EJEMPLO: Imprimimos los días de la semana**

```javascript
var diasDeLaSemana = [
    "lunes",
    "martes",
    "miercoles",
    "jueves",
    "viernes",
    "sábado",
    "domingo"
];
   
let diaSemana = 0; 
while (diaSemana < diasDeLaSemana.length) {
  console.log(diasDeLaSemana[diaSemana]);
  diaSemana++;
}

```

### 5) Bucle `do - while` :

**SINTAXIS**

```javascript
do
  statement
while (condition);
```

Mientras la condición `condition` sea verdadera, el `código` del cuerpo del bucle será ejecutado.

**EJEMPLO: Imprimimos los días de la semana**

```javascript
var diasDeLaSemana = [
    "lunes",
    "martes",
    "miercoles",
    "jueves",
    "viernes",
    "sábado",
    "domingo"
];
   
let diaSemana = 0; 
do {
    console.log(diasDeLaSemana[diaSemana]);
     diaSemana++;
} while (diaSemana < diasDeLaSemana.length)
```

\


Como vemos, el bucle **`do - while`** tiene una sintaxis similar al bucle **`while`** , pero casi al revés, ya que seguiría el concepto de "**haz esto mientras se cumple esta condición**", y precisamente esta condición se pone a lo último, o sea, que **la controla al final.**

\


**VENTAJAS**:

* El hecho de que **garantice que al menos va a recorrer el bucle una vez, proporciona información**.
* Permite definir l**a lógica del bucle antes de evaluar la condición**, lo que puede ser **más conveniente en ciertos escenarios**.\


**EJEMPLO DE APLICACIÓN**:

Típíco en **juegos**, cuando queremos que siempre haga el proceso al menos una vez. Por ej. un **jugador que juega y te aseguras de que lo haga al menos una vez,** y si sigue ganando, puede comprobarlo en esa condición **`while`** y puede seguir iterando.

\


**LIMITACIONES**:

* **Puede devolver `undefined`** Si ponemos que la variable iteradora `diaSemana` es **10**, nos devolvería **`undefined`** ; sin embargo con el bucle **`while`** **no imprimiría nada**. El bucle **`do - while`** siempre **va a ejecutar el programa al menos UNA VEZ** (el otro no haría nada porque la condición está puesta al principio, y no se cumple si ponemos diaSemana = 10).
* **Riesgo de bucles infinitos:**\
  Si la condición del `while` nunca se vuelve **falsa**, **el bucle se ejecutará indefinidamente**, lo que puede causar problemas en la aplicación. Es crucial **asegurarse de que la condición eventualmente se evalúe como falsa** para evitar este problema.
* **Menos común que otros bucles:** En comparación con los bucles **`for`** y **`while`**, el **`do...while`** se usa **con menos frecuencia**, ya que a menudo se puede lograr la misma lógica con los otros tipos de bucles.
* **Puede ser más difícil de entender:** Para algunos desarrolladores, la estructura del **`do...while`** **puede resultar menos intuitiva que otros bucles**, especialmente si no están familiarizados con su ejecución.

\

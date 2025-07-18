# 2 ¿Cuáles son las diferencias entre const, let y var?



### 1. Variable   var

* Durante muchos años, en JavaScript **sólo existía** la variable **`var`**.
* Cuando creamos un variable con **`var`**, estamos creando una **variable GLOBAL**, lo que significa que puede entrar en conflicto con otras variables, y hacer lo que se denomina como "**contaminar la variable global**".
  * Puede llevar mucho tiempo averiguar **qué está pasando exactamente** en el programa, y también el **solventar ese error de nombrado**.
  * Por tanto, **necesitamos controlar dónde están nuestras variables declaradas** y dónde tenemos acceso a ellas, pero con **`var`** esto es algo **muy difícil de hacer**.
  * Aunque te lo puedes encontrar o pueden existir situaciones donde puede ser útil, **hoy en día no tiene demasiado sentido utilizar** **`var`** en nuestro código.
* Otra diferencia particular de **`var`** es que **tolera redeclaraciones**:

**EJEMPLO 1 : `var` tolera redeclaraciones:**

```javascript
var user =  "Pete";
var user =  "John";
console.log(user); // John
```

**EJEMPLO 2: alcance de `var`;**

```javascript
var mensajeGlobal = "Hola, soy global!";

function mostrarMensaje() {
  console.log(mensajeGlobal); // Accede a la variable global
}

mostrarMensaje(); // Imprime "Hola, soy global!"
console.log(mensajeGlobal); // Imprime "Hola, soy global!"

if (true) {
  var dentroDeBloque = "Dentro de un bloque";
}

console.log(dentroDeBloque); 
// Imprime "Dentro de un bloque", porque var ignora el bloque
```

### 2. Variable   let

* **`let`** vino hace unos años, y se convirtió en una **mejor** manera de definir variables, ya que **no contaminaba el espacio de nombramiento global**.
* **`let`** permite **reasignar el valor** de la variable.
* Como consecuencia, era mucho más específico, estaba **más limitado**; si se creaba dentro de una función o se añadía a ella, **sólo estaría disponible en esa función:** no habría otros momentos en los que estuviera disponible.
* **`let`** limita el **alcance** de las variables **al bloque donde se definen**, evitando efectos secundarios no deseados en otros bloques de código.
* **`let`** **no permite redeclarar** la misma variable **en el mismo ámbito**, lo que ayuda a evitar errores.
* El alcance de bloque de **`let`** hace que el **código sea más fácil de entender y mantener.**
* **No tolera redeclaraciones**:

```javascript
let user;
let user;  // Identifier 'user' has already been declared
```

\


EJEMPLO DE **`let`** vs. **`var`**;

```javascript
var a = 5;
var b = 10;

if (a === 5) {
  let a = 4; // El alcance es dentro del bloque if
  var b = 1; // El alcance es global

  console.log(a);  // 4
  console.log(b);  // 1
} 

console.log(a); // 5 - sigue igual, let- cambia solo bloque if
console.log(b); // 1 - ha cambiado: var- alcance global
```

\


### 3. Variable   const

* La variable **`const`** es **la más nueva**, y es una abreviación de "**constante**".
* Su valor **no puede ser reasignado después de su inicialización**.
* Se ha convertido en **una de las más populares** a la hora de declarar variables. Se puede ver en los desarrolladores que **es la preferida por encima de las otras opciones** .
* En la **mayoría de aplicaciones** se ven sobre todo la **variable `const` y la variable `let`**.
* Por norma general en los programas modernos (especialmente en _**React**_**,&#x20;**_**Angular**_ o plataformas del estilo) se utiliza **la variable `const`.**

EJEMPLO DE **`const`**:

```javascript
const objeto = {  
nombre: "Ejemplo",  
valor: 10 };  
  
objeto.valor = 20; 
// Esto es válido, se puede modificar la propiedad de un objeto const. 

objeto = { nombre: "Nuevo", valor: 30 }; 
// Esto daría error, no se puede reasignar la constante objeto.
```

\


EJEMPLO DE **`const`** VS. **`let`**:\


**1) `const` : esta variable no se puede cambiar**^(\*1)^

```javascript
const casa  =  "Benidorm";  
console.log(casa);
  
casa = "Marbella";
console.log(casa);       

// Devuelve un error:
//           "TypeError: Assignment to constant variable. 
```

(\*1)\


<div align="left"><figure><img src=".gitbook/assets/iconoPrecauc (3).png" alt=""><figcaption></figcaption></figure></div>

**OJO!!** Si estamos utilizando la plataforma web **CODEPEN**, **no nos va a mostrar el error**, por ello en este caso deberíamos utilizar otras opciones, **como la consola del navegador.**\


**2)`let` : la variable se ha podido cambiar**

```javascript
let casa  =  "Benidorm";  
console.log(casa);   //devuelve: "Benidorm"
  
casa = "Marbella";
console.log(casa);  //devuelve:"Marbella"     
```

\


**BUENAS PRÁCTICAS**

* **La variable `const` debería ser nuestra mejor opción por defecto**.
* Si es demasiado específica, usaríamos **`let`**.
* Sin embargo, es difícil que veamos **`var`** en las aplicaciones modernas. No es que no pueda **haber casos en los que necesitemos una variable global**, en los que sería la ocasión para utiliar **`var`**, pero de normal no va a ser así.\


EN RESUMEN:

| Variable    | Propósito                                                                                                                                                                                                        |
| ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`var`**   | **solo** situaciones donde necesitas un **alcance de función específico** (o para funciones de práctica y aprendizaje de codificación). **Evitar el uso de `var`** debido a sus problemas de ámbito y _hoisting_ |
| **`let`**   | para variables que puedan ser **reasignadas**                                                                                                                                                                    |
| **`const`** | para declarar **variables que no van a cambiar** su valor a lo largo del programa                                                                                                                                |

\

# 5 ¿Qué hace el operador de extensión en JS?

**El operador de extensión** (también llamado operador de propagación) o **Spread Operator** es una herramienta muy potente de las plataformas más populares de JavaScript. Básicamente, **toma los elementos de un iterable** (arrays, cadenas, u objetos) **y los "desempaqueta" individualmente**.

**OBJETIVO**: Su objeto es facilitar **la manipulación y combinación de datos de manera concisa**. **SINTAXIS**: 3 puntos seguidos (...) de algún tipo de palabra.

### 1. CONVERTIR CADENAS EN ARRAYS

```javascript
let cadena = "Mundo";
let array = [...cadena];
console.log(array); // ["M", "u", "n", "d", "o"]
```

\


### 2. COMBINAR ARRAYS

a) Comparemos poniendo el **operador de extensión**:

```javascript
let numbers = [1,2,3,4];
let newNumbers = [8,9];

numbers.push(...newNumbers);
console.log(numbers); //imprime [ 1, 2, 3, 4, 5, 8, 9 ]
```



<div align="left"><figure><img src=".gitbook/assets/iconoPrecauc (6).png" alt=""><figcaption></figcaption></figure></div>

**OJO!!** Recordemos que **el método `push()` cambia la variable original.**\


b) **Si no pusiéramos la extensión ...** entonces lo añadiría como **un único** elemento, un **array (anidado**):

```javascript
let numbers = [1,2,3,4];
let newNumbers = [8,9];

numbers.push(newNumbers);
console.log(numbers); //imprime [ 1, 2, 3, 4, [ 8, 9 ] ]
```

precisamente por cómo JavaScript interpreta los arrays: **un conjunto de “cualquier tipo de datos”.** La solución, pues es utilizar el operador de extensión.

\


### 3. COPIAR ARRAYS

* Cuando trabajas con arrays basados en **React**, **Angular** y otras plataformas de JavaScript, se sobreentiende que **no tienes que hacer cambios en una estructura de datos ya creada**: esto se trata en realidad de una CONVENCIÓN COMÚN.
* Una variable declarada con **const** nos da precisamente esa seguridad, ya que nos daría error si más tarde en el programa intentamos cambiar la estructura de datos de esta variable.
* Otra situación que puede pasar, es que **añadamos un string** a algo en este array que contiene números, y luego **otra parte del programa considera que solo había números enteros** (porque en principio era así), y ejecuta un proceso sobre esa estructura: **nos daría error**.\


**BUENAS PRÁCTICAS**

* Lo más **limpio y seguro** es hacer una **copia** de esa variable original, y luego usar **let** para hacer nuestras modificaciones. De esta forma **evitamos crear los menos efectos secundarios posibles**
* Debido a que **el método `push()`, como ya hemos dicho, cambia la variable original**, si hacemos la siguiente asignación con la intención de realizar una copia, seguiríamos con **problema**:

**EJEMPLO con `push()`**

```javascript
const numbers = [1,2,3,4];
const updatedNumbers = numbers;

updatedNumbers.push(5);

console.log(numbers); //imprime  [ 1, 2, 3, 4, 5 ]
console.log(updatedNumbers);//imprime  [ 1, 2, 3, 4, 5 ]
```

Vemos que **cambia las dos variables**.\
\


<p align="right"></p>

**¿QUÉ ESTÁ PASANDO EXACTAMENTE?**

<div align="left"><figure><img src=".gitbook/assets/interrogacion.png" alt="" width="114"><figcaption></figcaption></figure></div>



Lo que está ocurriendo es que aquí **no está pasando una copia, sino una referencia**. Y lo que esto significa es que si haces una modificación en **updatedNumbers**, también lo haces en **numbers**, y como consecuencia estás **modificando también la variable original.**\
Tenemos **dos soluciones** a esto:\


#### a) Forma tradicional: añadir `slice()` a la variable original

El método `slice()` en JavaScript se utiliza para extraer una porción de una array. Cuando se llama **sin argumentos** toma todos los elementos del array, o sea, **crea una copia de todos los elementos del array original**.

**EJEMPLO - `slice()`**

```javascript
const numbers = [1,2,3,4];
const updatedNumbers = numbers.slice();

updatedNumbers.push(5);

console.log(numbers); //imprime  [ 1, 2, 3, 4]
console.log(updatedNumbers);//imprime  [ 1, 2, 3, 4, 5 ]
```

\


#### b) Forma moderna: operador de extensión

**SINTAXIS:**

`[…variableOriginal];`\


**EJEMPLO - operador de extensión:**

```javascript
const numbers = [1,2,3,4];
const updatedNumbers = [...numbers];

updatedNumbers.push(5);

console.log(numbers);  //imprime [ 1, 2, 3, 4 ]
console.log(updatedNumbers); //imprime [ 1, 2, 3, 4, 5 ]
```

\


Vemos que **cambia las dos variables**.\
\
\
\
\
&#xNAN;**¿FORMA TRADICIONAL O MODERNA?** \


<div align="left"><figure><img src=".gitbook/assets/interrogacion (1).png" alt="" width="114"><figcaption></figcaption></figure></div>



* Se ven **los dos tipos** de comportamientos en las aplicaciones reales, ya que los desarrolladores han aplicado ambos durante muchos años: el método **`slice()`** ha estado siempre **muy extendido**.
* Sin embargo, en los últimos años, y si miramos en las aplicaciones creadas en **Angular**, o **View**, se aprecia **cada vez con más frecuencia la predominancia del operador de extensión**.

Ambos funcionan de igual manera, pero quizá la **tendencia es a usar más la última forma más moderna.** No obstante es importante conocer los dos y tener ambas posibilidades.\
\


**NOTA**:\
El tipo de copia que se crea en estos casos es una **copia superficial**, en comparación con una **copia profunda** :

* una **copia superficial** (_shallow copy_) crea un nuevo objeto, pero los elementos internos (si son objetos o arrays) **son referenciados desde el objeto original**.
* una **copia profunda** (_deep copy_), por otro lado, crea un nuevo objeto y **copia recursivamente todos los elementos**, es decir, **incluyendo los objetos y arrays anidados**, para que no compartan referencias con el objeto original.\
  \


### 4. PASAR ARGUMENTOS A FUNCIONES

Esto es algo **muy común**. Para explicarlo, tomaremos de la biblioteca, el objeto **Math** (disponible en todo JavaScript), y utilizaremos **el método`max()`**. Este método:

* se utiliza para encontrar **el valor más grande de una lista de números**
* **si** se proporciona un argumento que **no es un número**, `Math.max()` **devuelve `NaN`** (Not a Number)

\


**EJEMPLO 1 - cómo funcióna `Math.max()`:**

```javascript
console.log(Math.max (1,5,1,10,2,3));  // devuelve 10 
```

Aquí estamos pasando una lista, como si fueran 6 argumentos.

\


**EJEMPLO 2 - pasando argumento como función:**

```javascript
const numbers = [1,5,1,10,2,3];
console.log(Math.max (numbers));  // NaN
```

Aquí la cosa es diferente: en este caso, interpreta que sólo estamos pasando **1 argumento**, cuyo tipo de dato es **un array, no un número**. Por esto el output de **NaN.**

Para arreglar esto, solo tenemos que añadir la **sintaxis de los tres puntos (…) del operador de extensión** y así poder implementar la **deconstrucción del array**:

**EJEMPLO 3 - operador de extensión**

```javascript
const numbers = [1,5,1,10,2,3];
console.log(Math.max (...numbers));  // 10
```

Finalmente conseguimos hacerlo: lo convierte en un conjunto de argumentos de función, que en este caso son **números.**

Este proceso **es muy típico en las plataformas modernas de JavaScript.**\


\


### 5. COMBINACIÓN DE PROPIEDADES DE VARIOS OBJETOS EN UNO NUEVO

Utilizando la **deconstrucción de objetos**, vamos a extraer los valores dentro del objeto de la variable, y los tenemos de dos tipos:

* Valores que son **fijos**: necesitamos que siempre estén ahí
* Otros valores **opcionales** que **pueden estar o no**, y tampoco conocemos el número de ello.

\


A) EXTRAYENDO LOS ELEMENTOS FIJOS:

```javascript
const {abridor,cerrador} = {
    abridor: 'Verlander',
    cerrador: 'Giles',
    relevo_1: 'Morton',
    relevo_2: 'Gregerson'
}

console.log(abridor); // "Verlander"
console.log(cerrador); // "Giles"
```

\
Para \*\*los fijos\*\*: ponemos \*\*las claves\*\* como parte del \*\*nombre de la variable.\*\*\
\


B) EXTRAYENDO LOS ELEMENTOS OPCIONALES O VARIABLES:

Añadiremos un elemento más como parte del nombre de la variable (de tipo "objeto"), haciendo uso del **operador de extensión** o _spread operator_:

```javascript
const {abridor,cerrador, ...relevos} = {
    abridor: 'Verlander',
    cerrador: 'Giles',
    relevo_1: 'Morton',
    relevo_2: 'Gregerson'
}

console.log(abridor); // "Verlander"
console.log(cerrador); // "Giles"
console.log(relevos); // { relevo_1: 'Morton', relevo_2: 'Gregerson' }
```

\


**A traves de la sintaxis `...elemento`**, haremos mapear este elemento **al resto de los elementos** que contiene la variable y nos **imprime un objeto con los pares la clave-valor del resto de los elementos**.

Como hemos visto en el punto nº 4, ésta es la forma que trabaja **la deconstrucción**:

* si pasamos un valor tal como `abridor`, lo busca en la variable (que es un objeto) y encuentra la clave, la mapea e imprime su valor.
* **Los tres puntos `...` crea un grupo abierto con un número de elementos indeterminado**, que mapeará al resto de elementos en cuanto creamos un variable para ello.

Es una de las formas más comunes de hacer **la deconstrucción de objetos** utilizado por muchas plataformas como _**React**_ cuando **no sabemos cuántos argumentos habrá** y necesitamos extraer todo lo que haya, con el fin de **guardarlo en una variable que podemos utilizar más tarde**.



<div align="left"><figure><img src=".gitbook/assets/iconoPrecauc (7).png" alt=""><figcaption></figcaption></figure></div>

**OJO!! El operador de extensión ... debe colocarse al final de los demás elementos del objeto**. Generaríamos un error si tratamos de hacer `const {abridor, ...relevos, cerrador}....`. Este error, diría algo así como `// SyntaxError: Rest element must be last element`.\

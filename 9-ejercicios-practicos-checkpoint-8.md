# 9) EJERCICIOS PRÁCTICOS CHECKPOINT 8

```js
/*  EJERCICIO 1
 Cree un bucle for en JS que imprima cada nombre en esta lista.
 miLista = “velma”, “exploradora”, “jane”, “john”, “harry”
 */

 const miLista = [
   "velma",
   "exploradora",
   "jane",
   "john",
   "harry"]; 

miLista.forEach((elemento) => {
  console.log(elemento);
  });


/*  EJERCICIO 2

Cree un bucle while que recorra la misma lista 
y también imprima los nombres. 
Nota: Recuerda crear un contador para que el ciclo no sea infinito.
*/


var miDiario = ["lunes","martes","miércoles", "jueves", "sabado", "domingo"];

var item = 0;
while (item < miDiario.length) {
  console.log(miDiario[item]); item++;
}


/*  EJERCICIO 3
Cree una función de flecha que devuelva "Hola mundo".
*/

holaMundo = () => {console.log("Hola mundo")};
holaMundo();

```

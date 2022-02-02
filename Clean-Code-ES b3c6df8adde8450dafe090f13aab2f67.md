# Clean-Code-ES

### Este articulo es una recopilación de la información más relevante de [Clean Code](https://softwarecrafters.io/javascript/clean-code-javascript) escrito por Miguel A. Gómez.

Adjunto mi articulo Clean-Code-EN **en inglés,** lo puedes visitar **[aquí](https://www.notion.so/Clean-Code-e810e660fe0d4db68d8af91ad9a341d5).**

---

### Deuda técnica

Una deuda técnica es escribir código el cual no esta totalmente optimizado, tiene un corto ciclo de vida, no ha sido testeado, debe ser entregado con urgencia, no es escalable, legible o directamente es malo. Tengo un articulo que puedes visitar [aquí](https://www.notion.so/Data-Structures-and-Algorithms-e11edc7759404c35bfae452186def455) para leer más acerca de **algoritmos y estructuras de datos** (en inglés).

Existen ciertas deudas técnicas, algunas son más prudentes que otras, pero todas tienen algo en común, **deben pagarse.** A continuación te mostraré un esquema dónde puedes apreciar cada una de ellas junto a su explicación.

![Esquema por Martin Fowler](Clean-Code-ES%20b3c6df8adde8450dafe090f13aab2f67/Untitled.png)

Esquema por Martin Fowler

- Deuda imprudente y deliberada:
    - Es llevada a cabo por un mal desarrollador o bien, un proyecto de bajo presupuesto, ya que se esta conciente de la poca o nula escalabilidad del código.
- Deuda prudente e inadvertida:
    - Es muy peligrosa, se lleva a cabo por desarrolladores Junior, falta de experiencia y falta de conocimiento.
- Deuda prudente y deliberada:
    - En ocasiones es inteligente hacer uso moderado de ella, tiene como principal motivo el acelero de desarrollo, sin embargo **debe pagarse cuanto antes**.
- Deuda prudente e inadvertida:
    - Al concluir un proyecto el desarrollador concientiza que pudo haber implementado mejores soluciones y se debe valorar si implementar dicha solución o posponer.

### Refactorizar

Es muy común usar este término entre desarrolladores, implica pagar la deuda técnica y así mejorar la calidad de software. 

Para considerar pagar la deuda técnica es necesario comprender lo que esto conlleva, tal como es el testing, de no implementarlo podría hacer perder mucho tiempo en el desarrollo de nuevas soluciones ya que automatiza cualquier tarea repetitiva. Recuerda **no** ser el típico desarrollador ~~**“Si funciona no lo toques”.**~~

Siempre hay que valorar la necesidad de un proyecto, ya que un refactor no siempre es la mejor opción, ya que en medidas más extremas se debería considerar cambiar la arquitectura que lleva el proyecto.

---

### Clean Code

![Meme por osnews.com/comics](Clean-Code-ES%20b3c6df8adde8450dafe090f13aab2f67/Untitled%201.png)

Meme por osnews.com/comics

El principio de clean code es que pueda ser entendido por un desarrollador que no seas tú (o tú mismo en el futuro). 

Uno de los errores más comunes de los desarrolladores junior es no pensar a futuro y escribir código como no de lugar, y este es uno de los errores que más dinero cuesta al mantenimiento del software.

 

### Variables, nombres y ámbito

Una de las cosas más díficiles de programar es elegir los nombres apropiados para determinada variable, función o clase, al mismo tiempo es una de las más importantes ya que el código debe leerse con la misma facilidad al leer un texto. Cada nombre se debe elegir con basto cuidado para que sea autoexpresivo y de vida a nuestro código

### Uso correcto de let, const y var

- Const
    
    Tiene como proposito general no modificar el valor el cual esta siendo almacenado dentro de sí, aunque los tipos de datos **primitivos** pueden ser mutables.
    
    ```jsx
    const rating = 10; //no se puede modificar este dato
    rating = 8 // error
    const data = [ 1, 2, 3 ] //no se puede modificar, pero si mutar
    data = 1,2,3 // error
    data.push(40) // output: [ 1, 2, 3, 40 ] 
    const dataobj = { 'github': 'https://github.com/HendrickGH' }
    dataobj = [] // error
    dataobj = {} // error (esto porque se esta reasignando un valor)
    dataobj.twitter = 'https://twitter.com/HendrickGalarza' 
    /* output: {
       'github': 'https://github.com/HendrickGH', 
       'twitter': 'https://twitter.com/HendrickGalarza' 
    } */
    ```
    
- Let
    
    Tiene como proposito ser modificable tanto como a nivel de mutación como a nivel de tipo de dato o valor, es mucho menos usada de const, aunque tiene ocasiones en que puede ser muy útil
    
    ```jsx
    let rating = 10; //modificable
    rating = 8; // output: 8
    rating = [] // output: []
    rating = {} // output: {}
    rating = 'Hello there!' // output: 'Hello there!' 
    ```
    
- Var
    
    Muy similar a let sin embargo debe ser **evitada** a toda costa ya que modifica el scope global `window`o `this` además de que no crea variables a nivel de bloque, algo que a la larga puede generar muchos problemas en sobreescritura de valores.
    

### Nombres pronunciables y expresivos

Como se hizo incapie al inicio, se debe saber como elegir el nombre de cualquier cosa, no importa que sea, además se debe escribir en inglés y priorizando el camelCase.

```jsx
//mal nombre
const alumnosSemestre = [ 10, 9, 6 ]
//mejor nombre
const calificaciones = [ 10, 9, 6 ]
```

### Nombres según el tipo de dato

- Arrays
    
    Se debe pluralizar el nombre de la variable
    
    ```jsx
    //mal 
    const fruit = [ 'manzana', 'platano', 'fresa' ]
    //mejor
    const fruits = [ 'manzana', 'platano', 'fresa' ]
    ```
    
- Boolean
    
    Ya que solo pueden tener 2 valores, es una excelente idea hacer uso de los prefijos *is, has, can*
    
    ```jsx
    //mal
    let close = true
    let read = false
    let food = true
    //mejor
    let isClose = true
    let canRead = false
    let hasFood = true
    ```
    
- Números
    
    Es buena idea escribir los prefijos *min, max, total*
    
    ```jsx
    //mal
    let fruits = 3 
    //mejor
    let totalFruits = 3
    let maxFruits = 3
    let minFruits = 3
    ```
    
- Funciones
    
    Las funciones ejecutan acciones por lo tanto deben nombrarse con el verbo que les representa seguido del sustantivo para así ser concisos y descriptivos. Por tanto debe expresar lo que hace. 
    
    ```jsx
    //mal
    createTableInClients()
    submitPostUserValid()
    submitPostPageValid()
    errorEmpty()
    //mejor
    createTable()
    submitPost()
    errorData()
    
    //si dichas funciones acceden o modifican algo
    //mejor
    setData()
    getData()
    ```
    

### Scope de las variables

Hace referencia a que tanto alcance puede tener una variable así como su vida útil. En javascript existen tres tipos de scopes. 

- Ámbito global
    
    Para las variables que no esten dentro de un bloque de función estaran accesibles en cualquier parte de la aplicación, en vanilla js es muy usado para seleccionar los elementos del DOM. 
    
    ```jsx
    const price = document.querySelector('.price');
    const setPrice = textPrice => {
    		price.textContent = textPrice; 
    }
    ```
    
- Ámbito de bloque
    
    Estas se delimitan a las llaves las cuales estan dentro de las funciones, condicionales, bucles o métodos
    
    ```jsx
    const setPrice = textPrice => {
    		const isOffer = false; //output: false
    		isOffer && price.textContent = textPrice; 
    }
    //output: is not defined (null)
    ```
    
- Ámbito dinámico
    
    Si existe una variable en el ámbito global pero creamos una variable con el mismo nombre en un ámbito de bloque, tomará esta.
    
    ```jsx
    const price = document.querySelector('.price')
    const setPrice = textPrice => {
    		const price = document.querySelector('.price.offer'); 
    		price.textContent = textPrice //afecta solo a la variable definida en la función
    }
    ```
    

### Hoisting

El hoisting es el orden en que las variable y funciones se asignan en memoria en el tiempo de compilación. Una ventaja y desventaja del hoisting es que no importa (o si) dónde declares una función, podrás (o no) usarla. 

Cuando se declara una función imperativa puede ser utilizada en cualquier sitio de la aplicación.

```jsx
greet(); // 'Hello world!'
function greet(){
	const greeting = 'Hello world!'; 
	return greeting
}
```

Sin embargo esto no sucede de la misma forma si es declarada de manera expresiva

```jsx
greet(); // greet is not defined
const greet = () => {
	const greeting = 'Hello world!'; 
	return greeting; 
}
greet(); // 'Hello world!'
```

Aunque en este ejemplo no funcionara debido a que el error que genera la primera llamada a la función detiene la ejecución del programa, cuando una función es expresiva, solo puede ser utilizada después de su creación o en caso contrario tendremos problemas de hoisting.

En el caso de las variables es mucho más inesperado, ya que solo aplica a la declaración y no a la asignación

```jsx
var greet = 'Hi!'; 
(function(){
	console.log(greet) //undefined
	var greet = 'Hello world!'; 
	console.log(greet) // 'Hello world!'
})()
```

El comportamiento esperado sería como primer instancia mostrar en consola ‘Hi!’ pero esto no es así debido a la elevación de la declaración de la variable, el intérprete técnicamente hace esto: 

```jsx
var greet = 'Hi!'; 
(function(){
	var greet; 
	console.log(greet) //undefined
	greet = 'Hello world!'; 
	console.log(greet) // 'Hello world!'
})()
```

Recuerda que es mala idea nombrar variables con el mismo nombre y además es mala práctica usar var, este ejemplo es meramente demostrativo por sobre el hoisting.

### Funciones

> “Sabemos que estamos desarrollando código limpio cuando cada función hace
exactamente lo que su nombre indica”. – Ward Cunningham
> 

Una función es una entidad organizativa para desarrollar software de manera óptima, además de transmitir claramente cual es el objetivo de las mismas, en esta sección se demostrará como se deben definir: declarativamente, expresivamente y las funciones flecha. 

- Declaración de una función
    
    La clásica manera de crear una función en javascript como en otros tantos lenguajes es con la palabra reservada `function`, puede o no tener parametros y la lógica que lleva dentro es lo que ejecutara cada que sea llamada, además, puede devolver cierto valor con la palabra reservada `this` 
    
    ```jsx
    function doSomething(){
    	return 'Doing something'; 
    }
    ```
    

 

- Expresión de una función
    
    En este caso se le asigna una función a una variable, este tipo de funciones es súper utilizada en librerías para javascript como React, Angular, Vue, Svelte entre muchas otras más.
    
    ```jsx
    const doSomething = () => {
    	return 'Do something'; 
    }
    ```
    
- Expresiones con funciones flecha
    
    Muy similar a la expresión, sin embargo es utilizada cuando se hace alguna operación corta, tiene el propósito de ser mucho más legible y concisa, sin embargo no se debe abusar de ella haciendo múltiples encadenamientos ya sean de objetos, arreglos o strings, ya que pierde el propósito de ser legible
    
    ```jsx
    const doDomething = () => 'Doing something'; 
    ```
    
    Súper útiles para funciones en línea justo como así. 
    
    ```jsx
    arr.map(n => n * 2); 
    ```
    
    Lo cual nos ahorraría acudir a las expresiones comunes
    
    ```jsx
    arr.map((n) => {
    	return n * 2; 
    })
    ```
    
    ```jsx
    const noThis = () => this; //window
    ```
    
    Aunque existen diferentes casos en que referencia a otros objetos padres
    
    ```jsx
    const decrementer = {
    		number: 100,
    		decrease() {
    			(() => --this.number)() // number = 99
    		}
    }
    ```
    
    ```jsx
    const decrementer = {
    		number: 100,
    		decrease() {
    			(function(){ 
    					--this.number
    			})() // number = NaN
    		}
    }
    ```
    

### El casi nulo uso de this en las funciones de expresión

Una característica que diferencia de las funciones tradicionales es que técnicamente no podemos hacer uso de this, ya que va a referenciar al objeto padre, en la mayoría de los casos, el ámbito global del navegador

Al invocar a this, se pierde el contacto con el objeto padre ya que en el caso de las funciones tradicionales, this referencia a si mismo. 

### Parámetros y argumentos

Los argumentos son valores que llaman de las funciones y los parámetros son variables nombradas que reciben estos nombres dentro de las funciones

```jsx
const getLength = str => str.length // str representa los parámetros
getLength('Soy un argumento') 
// al invocar la función se le pasa un valor, este (o estos) son los argumentos
```

### Parámetros por defecto

Desde ES6 se permite establecer parámetros por defecto en las funciones, esto para prevenir resultados inesperados

```jsx
const greet = (text = 'world') => ('hello' + text)
greet() // 'hello world'
greet(undefined) // 'hello world' (ya que undefined es igual a no pasar nada)
greet('Hendrick') // 'hello hendrick'
```

### Parámetro rest y operador spread

Este operador (...) puede ser rest o bien spread, dependiendo el uso que se le dé. 

Por un lado el parámetro rest se utiliza cuando en una función se tienen determinado número de argumentos, sin embargo al llamar la función se excede el número de parámetros, y de esta manera, se almacenan todos los argumentos en el último parámetro. 

```jsx
const add = (...arr) => arr.forEach(e => console.log(e)); 
add(20, 'Hola', false, true, callback) // 20, 'Hola', false, true, callback(){...}
```

Sin embargo antes de ES6 no existia el parámetro rest y en su lugar era utilizada la palabra reservada **arguments**, pero **no es aconsejable** su uso ya que aunque aparente ser un array, no lo es ya que no implementa las funciones de un array cualquiera, además puede sobrescribirse.

Por otro lado el operador spread divide un objeto o un arreglo en múltiples elementos, lo que permite expandir expresiones donde esperen múltiples valores. 

```jsx
const hacerCosas(x, y, z){}
const argumentos = [0, 1, 2]
hacerCosas(...argumentos) 
```

Además con este operador podemos copiar arreglos u objetos con una limpia sintaxis. 

```jsx
const tareas = { 
			programar: 'Hacer una maqueta de facebook', 
			leer: 'Leer codigo limpio',
		  dormir: '8 horas' 
}
const tareasCopia = { ...tareas } // copia el objeto
const tareasNuevas = { ...tareas, jugar: '3 partidas de ajedres' } 
// copia el objeto y añade nuevas propiedades

const arreglo = [1,2,3,4,5,6,]
const arregloCopia = [ ...arreglo ] // [ 1,2,3,4,5,6 ]
const arregloMas = [ ...arreglo, 7, 8, 9 ] // [1,2,3,4,5,6,7,8,9]
```

### Tamaño y niveles de identación

Por norma general, las funciones deben hacer una sola cosa y claro, hacerla bien, se debe evitar la anidación de código y con ello evitar el código spaguetti además de mejorar la lejibilidad y mantenibilidad de la misma. 

```jsx
const getPayAmount = () => {
let result;
if (isDead){
		result = deadAmount();
	}
	else {
	if (isSeparated){
		result = separatedAmount();
	}
	else {
	if (isRetired){
		result = retiredAmount();
	}
	else{
			result = normalPayAmount();
			}
		}
	}
	return result;
}
```

### Cláusulas de guarda

A esto yo le llamo la salida rápida, verifica cualquier cosa antes de ejecutar cualquier código, como extra evita la sobre anidación

```jsx
const getPayAmount = () => {
	if (isDead)
		return deadAmount();
	if (isSeparated)
		return separatedAmount();
	if (isRetired)
		return retiredAmount();
	return normalPayAmount();
}
```

### No uses else

Siempre que sea posible evitar este tipo de anidamiento, en vez de ello se puede ser más declarativo y hacer uso del operador ternario, lo que da lugar a un código más legible, compresivo y expresivo. 

```jsx
const isRunning = true; 
// mala práctica
if(isRunning){
	stop()
}else{
	run()
}
// mejor práctica
isRunning ? stop() : run() 
```

### Transparencia referencial

Se dice que una función cumple con este principio si con el mismo valor de entrada produce siempre el mismo valor de salida, a esto se le llama función pura, y son la base de la programación funcional.

```jsx
const arr = [1, 2, 3, 4]; 
const sinTransparencia = (str) => {
	return [ ...str, ...arr.splice(1, 3) ]
}
sinTransparencia('Hola') // [ 'H', 'o', 'l', 'a', 2, 3, 4 ] arr = 1 

const conTransparencia = (str, arr) => [ ...str, ...arr.splice(1, 3) ] 
conTransparencia('Hola', [1, 2, 3, 4]) 
// [ 'H', 'o', 'l', 'a', 2, 3, 4 ] arr = [1,2,3,4] 
```

En el segundo ejemplo al tener como parametro a arr no afecta a arr en el ámbito global y por tanto no hay efectos secundarios.

### Principio DRY

Tener múltiples veces suele ser un grave problema, ya que puede deteriorar el código o hacerlo más lento o ilegible, es por ello que se debe hacer uso del principio DRY (Don’t repeat yourself), el cual significa “no repitas lo mismo”.

Como NO hacer las cosas: 

```jsx
const reportData = {
	name: "Hendrick",
	createdAt: new Date(), 
	purchases: 100,
	conversionRate: 10, 
}
function withOutDry(){
	function showReport(reportData){
		const reportFormatted = `
			Name: ${reportData.name}
			CreatedAt: ${reportData.createdAt}
			Purchases: ${reportData.purchases}
			Conversion rate: ${reportData.conversionRate}%
		`;
		console.log("Show report: ", reportFormatted); 
	}
	function saveReport(reportData){
		const reportFormatted = `
			Name: ${reportData.name}
			CreatedAt: ${reportData.createdAt}
			Purchases: ${reportData.purchases}
			Conversion rate: ${reportData.conversionRate}%
		`;
		console.log("Saving report...", reportFormatted)
	}
	showReport(reportData); 
	saveReport(reportData); 
}
```

Cómo hacer las cosas:

```jsx
const reportData = {
	name: "Hendrick",
	createdAt: new Date(), 
	purchases: 100,
	conversionRate: 10, 
}
function withDry(){
	function formatReport(reportData){
		return `
			Name: ${reportData.name}
			CreatedAt: ${reportData.createdAt}
			Purchases: ${reportData.purchases}
			Conversion rate: ${reportData.conversionRate}%			
		`;
	}
	function showReport(reportData){
		console.log("Showing report: ", formatReport(reportData)); 
	}
	function saveReport(reportData){
		console.log("Saving report: ", formatReport(reportData)); 
	}
	showReport(reportData); 
	saveReport(reportData); 
}
```

### Command-Query Separation (CQS)

La idea de este principio es dividir las funciones en un sistema de dos categorías

- Consultas (queries): Son funciones puras, solo devuelven un valor sin alterar el estado del sistema.
- Comandos (commands): Son funciones que generan efectos colaterales, también son conocidos como modificadores (modifiers) o mutadores (mutators). No deberían devolver ningún valor.

### Algoritmos eficientes

¿Cómo saber si el código tiene un rendimiento adecuado? Para ello se debe conocer la notación Big O, súper importante para cualquier desarrollador, agnóstico a la tecnología que se utilice.

### Big O Notation

Se trata de una aproximación matemática para determinar el comportamiento de un algoritmo, tanto en tiempo como espacio, en otras palabras cuanto tardara en ejecutarse o cuanta memoria necesita basado en el número de elementos que procesara.

Notaciones más comunes: 

- O(1) constante, es una operación que no depende del número de datos, siempre realizará la misma cantidad de operaciones.
- O(log n) logarítmica, se da en casos en que no es necesario recorrer toda la información, por ejemplo una búsqueda binaria.
- O(n) lineal: el tiempo de ejecución es proporcional al tamaño de los datos, si la información tiene una longitud de 100 elementos entonces la cantidad de instrucciones será proporcional a 100.
- O(n^2) cuadrática: Algoritmos dónde existen iteraciones anidadas, se recomienda encarecidamente hacer el menor uso posible de este.
- O(2^n) exponencial: son funciones que multiplican su complejidad con cada elemento añadido, son mejor conocidas como recursivas múltiples, no son recomendables.
- O(n!) explosión combinatoria: Son algoritmos que son literalmente imposible de resolver y de ejecutar posiblemente se detenta la aplicación y en casos extremos el ordenador.

### Comentarios y formato

### Evitar el uso de comentarios

> “No comentes el código mal escrito, mejor reescríbelo” -Brian W. Kernighan
> 

Cuando te veas en la necesidad de explicar tu código por comentarios, posiblemente no es lo suficientemente auto explicativo, por tanto se deben buscar alternativas como renombrar las funciones y o variables, aunque puede haber excepciones por ejemplo al usar librerías, evitar el uso de comentarios es la regla, no la excepción.

### Me quede en la página 67, formato coherente:)
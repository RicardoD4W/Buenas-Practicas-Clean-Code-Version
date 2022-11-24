# Comentarios
## 1. Comenta únicamente la lógica de negocio que es compleja
Se dice que un buen código debería comentarse por si mismo. **Comentaremos solo logicas que consideremos complejas**


Mal uso:

```javascript
    
//valor 1
let n1;

//valor2
let n2;

//funcion que devuelve un suma
function s(n1, n2) {
    return n1 + n2:
}


```

Buen uso:

```javascript

let numerol;
let numeroz;

//funcion que devuelve un suma
function suma (numerol, numero2) {
    return numero1 + numero2;
}


```
---
## 2. No dejes código comentado en tu repositorio
Si comenta un código porque en breves o algun día lo vas a necesitas... **borralo**. El código que borres consta en alguna de tus versiones de tu código fuente, **usa git**


Mal uso:

```javascript

function suma() { }

//function resta()) {}

//function divide () {}


```

Buen uso:

```javascript
function suma() { }

//function resta()) {}

//function divide () {}
```
---
## 3. No hagas un diario de comentarios
No hay motivo alguno para tener código muerto, código comentado y aún menos, un diadrio o resumen de modificaciones en tus comentarios.


Mal uso:

```javascript
/**
* 2022-10-25: funcion resta terminada
* 2022-10-01: funcion divide terminada
* 2022-10-03: funcion multiplica terminada
*/

function suma(a, b) {
    return a + b;
}
```

Buen uso:

```javascript
function suma(a, b) {
    return a + b;
}
```
---
## 4. Evita los marcadores de secciones
Evidente, el nombre de las propias variables, fuciones, clases... deberian de ser lo **suficientemente claro** para ser entendible

Mal uso:

```javascript
/////////////////////////////////////////////
//Funcion suma
/////////////////////////////////////////////
function suma(a, b) {
    return a + b:
}

/////////////////////////////////////////////
//Funcion resta
/////////////////////////////////////////////
function resta(a, b) {
    return a - b;
}
```

Buen uso:

```javascript
function suma(a, b) {
    return a + b:
}

function resta(a, b) {
    return a - b;
}
```
---


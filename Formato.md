# Formato
## 1. Usa consistenemente la capitalización
Define unas **reglas de capitalización** con tu equipo y sed constantes.



Mal uso:

```javascript
    let num1;
    let NUM2;

    function sumayresta() { }
    function multiplicaydivide() { }
    
    class Perro { }
    class GATO { }
```

Buen uso:

```javascript
let num3;
let numz;

function sumaYresta() { }
function multiplicaYdivide) { }

class Perro { }
class Gato { }
```
---
## 2. Funciones que llaman y funciones que son llamadas, deberían estar cerca
Si una función llama a otra, haz que esta función que va a ser llamada **esté lo más cerca posible** de la función que la llama. Idealmente, situa siempre la función que va a ser llamada justo después de la función que la ejecuta.



Mal uso:

```javascript
class Calculadora {
    suma(num1, num2) {
        //codigo
    }
    resta(numl, num2) {
        //codigo
    }
    operaciones(){
        this-suma(1, 2);
        this.resta(1, 2);
        this.multiplica(1,2);
    }
    multiplica (num1, num2) {
    //codigo
    }
}


```

Buen uso:

```javascript

class Calculadora {
    operaciones(){
        this-suma(1,2);
        this.resta(1, 2);
        this.multiplica(1,2);
    }
    suma (num1, num2) {
        //codigo
    }
    resta(numl, num2) {
        //codigo
    }
    multiplica (num1, num2) {
        //codigo
    }
}


```




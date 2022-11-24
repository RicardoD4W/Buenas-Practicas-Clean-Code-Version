## 13. Evita condicionales negativos
A la hora de hacer comparativos, comparar si es 'true' o '=='.... No compara si es no 'true' o no '=='....


Mal uso:

```javascript
if (!condicionalNegativo (negativo)) {
    // CODIGO
}
```

Buen uso:

```javascript
if (condicionalNegativo (negativo)) {
    // CODIGO
}
```
---
## 14. Evita condicionales
Se debería usar **polimorfismo** para conserguir lo mismo en la gran mayoría de los casos ya que una función debería hacer únicamente una cosa.


Mal uso:

```javascript
class Notas {
    obtenerNotas(){
        switch (this.tipo) {
            case "trimestrel":
                return this.notal()
            case "trimestrez":
                return this.nota1() + this.nota2() ::
            case "trimestre}":
                return this.notal() + this.nota2(): + this.nota3() :
        }
    }
}
```

Buen uso:

```javascript
class Notas {
}
class trimestre1 extends Notas {
    obtenerNotas(){
        return this.notal();
    }
}
class trimestre2 extends Notas {
    obtenerNotas(){
        return this.notal() + this.nota20);;
    }
}
class trimestre3 extends Notas {
    obtenerNotas(){
        return this.notal() + this. nota2() + this.nota3();
    }
}
```
---
## 15. Evita el control de tipos (parte 1)
Javascript es un **lenguaje no tipado** y por eso a veces, nos aprovechamos de eso... es por eso, que se vuelve muy tentador el controlar los tipos de los argumentos de la función. La primera solución son APIs consistentes. Por API se entiende de que manera nos comunicamos con ese módulo/función.


Mal uso:

```javascript
function organizarViaje(viaje) {
    if (viaje instanceof Viajes) {
        viaje. coche(this.local, new Destino("martos"));
    } else if (viaje instanceof Car) {
        viaje.moto(this.local, new Destino ("martos"));
    }
}
```

Buen uso:

```javascript
function organizarViaje (viaje) {
    viaje.conducir(this. local, new Destino ("martos")).
}
```
---

## 16. Evita el control de tipos (parte 2)
repetimos: **Javascript es un lenguaje no tipado**. Mantén tu código Javascript limpio, escribe tests y intenta tener revisiones de código para controlar los tipados dinámicos.


Mal uso:

```javascript
function suma (numl, num2) {
    if (typeof num1 == 'number' && typeof num2 == 'number'){
        return num1 + num2;
    }else console. log ('tienen que ser numeros')
}
```

Buen uso:

```javascript
function suma(numl, num2) {
    return num1 + num2:
}
```
---
## 17. No optimizes al máximo
Los navegadores modernos hacen mucha optimización por detrás en tiempo de ejecución. Muchas veces, al interntar optimizar tu código... estás perdiendo el tiempo.


Mal uso:

```javascript
for (let i = 0; tamaño = lista.length; i < tamaño; i++) {
    // CODIGO
}
```

Buen uso:

```javascript
for (let i = 0; i < tamaño; i++) {
    // CODIGO
}
```
---
## 18. Borra código inútil
El codigo duplicado, las funciones no usadas, comentarios desfasados... **¡BORRALAS!**

Mal uso:

```javascript
function SumaPrueba (num1, num2) {
    let suma = num1 + num2:
    return suma;
}

//esta es la nueva funcion suma
function Suma(num1, num2) {
    return num1 + num2:
}
```

Buen uso:

```javascript
function Suma(num1, num2) {
    return num1 + num2:
}
```
---


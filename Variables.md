# Variables

## 1. Utilizar nombres fáciles de pronunciar y con sentido:

A la hora de declarar variables, es preferible utilizar **nombres descriptivos**, ya que así podremos encontrarlas fácilmente, y a la hora de modificar el código, será más fácil intuir qué valores incluyen.

Mal uso:
```javascript
let tknusr = ASbh479XFR;
```

Buen uso:
```javascript
let tokenUsuario = ASbh479XFR;
```

---

## 2. Utilizar el mismo tipo de vocabulario para el mismo tipo de variables:

Si las variables tienen un **fin parecido**, es aconsejable que se llamen de **forma parecida**, para evitar errores y confusiones.

Mal uso:
```javascript
let nombreUsuario = "";
let datoTecnico = "";
let nameAdmin = "";
```

Buen uso:
```javascript
let nombreUsuario = "";
let nombreTecnico = "";
let nombreAdmin = "";
```

---

## 3. Utilizar nombres que puedan ser buscados: 

El código debe ser legible y se debe poder buscar en él, por lo que si no creamos variables significativas, estaremos entorpeciendo su lectura. Esto además puede dificultarnos encontrar posibles errores.

Mal uso:
```javascript
function calcularAreaCircunferencia(pi, radio) {
    let area = pi * Math.pow(radio, 2);
    return area.toFixed(2)
}

let area = calcularAreaCircunferencia(3.14159265359, 3);
```

Buen uso:
```javascript
function calcularAreaCircunferencia(pi, radio) {
    let area = pi * Math.pow(radio, 2);
    return area.toFixed(2)
}

const PI = 3.14159265359;
const radio = 3;

let area = calcularAreaCircunferencia(PI, radio);
```

---
## 4. Utilizar variables explicativas:

Cuando nos encontramos ante un código complejo de entender, es recomendable utilizar variables explicativas. Es decir, deben tener un nombre por el que se pueda intuir su propósito.

Mal uso:
```javascript
const direccion = "Calle Mallorca, Barcelona 95014";
const expresionRegularCodigoPostalCiudad = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
guardarCP(
  direccion.match(expresionRegularCodigoPostalCiudad)[1],
  direccion.match(expresionRegularCodigoPostalCiudad)[2]
);
```

Buen uso:
```javascript
const direccion = "One Infinite Loop, Cupertino 95014";
const expresionRegularCodigoPostalCiudad = /^[^,\\]+[,\\\s]+(.+?)\s*(\d{5})?$/;
const [, ciudad, codigoPostal] =
  direccion.match(expresionRegularCodigoPostalCiudad) || [];
guardarCP(ciudad, codigoPostal);
```

---
## 5. Evitar relaciones mentales:

Para entender mejor el código, nombrar variables de forma explícita es más claro y útil que hacerlo de forma implícita, ya que no podrás comprender correctamente a lo que te estás refiriendo.

Mal uso:
```javascript
const paises = ["España", "Italia", "Alemania"];
paises.forEach(a => {
  ordenarPaises();
  ponerEnMayusculas();
  //...
  //...
  dispatch(a);
});
```

Buen uso:
```javascript
const paises = ["España", "Italia", "Alemania"];
paises.forEach(ubicacion => {
  ordenarPaises();
  ponerEnMayusculas();
  //...
  //...
  dispatch(ubicacion);
});
```

---
## 6. No añadas contexto innecesario:

Si el nombre de tu clase u objeto hace alusión a algo en concreto, no es necesario repetirlo en el resto de nombres de variables o funciones.

Mal uso:
```javascript
const Movil = {
  marcaMovil: "Samsung",
  soMovil: "Android", 
  colorMovil: "Negro
};

function ponerFundaMovil(movil){
  movil.fundaMovilColor = "Rojo";
}
```

Buen uso:
```javascript
const Movil = {
  marca: "Samsung",
  so: "Android", 
  color: "Negro
};

function ponerFunda(movil){
  movil.funda = "Rojo";
}
```

---
## 7. Utilizar argumentos por defecto en vez de circuitos cortos o condicionales:

Al utilizar argumentos por defecto, el código se vuelve más limpio y, a la vez, se evita el uso de los cortocircuitos (||, &&, ??) que, a veces, puede alterar el valor de la variable.

Mal uso:
```javascript
function crearAppFarmacia(nombre){
  const nombreAppFarmacia = nombre || "SendSalud";
}
```

Buen uso:
```javascript
function crearAppFarmacia(nombre = "SendSalud"){
  // ...
}
```

---
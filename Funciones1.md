# FUNCIONES
## Argumentos de una función (idealmente 2 o menos)

Lo ideal es en una funcion es que los argumentos sean 2 o menos aunque se pueden pasar tantos parametros como queramos separados por comas.


Mal uso:

```
function crearMenu(titulo, cuerpo, textoDelBoton, cancelable) {
  // ...
}
```

Buen uso:

```
function crearMenu({ titulo, cuerpo, textoDelBoton, cancelable }) {
  // ...
}

crearMenu({
  titulo: "Foo",
  cuerpo: "Bar",
  textoDelBoton: "Baz",
  cancelable: true
});
```
---

## Las funciones deberían hacer una cosa.

Es preferible tener funiones especificas a pesar de tener mas funciones en el codigo pero esto conlleva a que el codigo este mas limpio y sea mas facil de entender.


Mal uso:

```
function enviarCorreoAClientes(clientes) {
  clientes.forEach(cliente => {
    const historicoDelCliente = baseDatos.buscar(cliente);
    if (historicoDelCliente.estaActivo()) {
      enviarEmail(cliente);
    }
  });
}
```

Buen uso:

```
function enviarCorreoClientesActivos(clientes) {
  clientes.filter(esClienteActive).forEach(enviarEmail);
}

function esClienteActivo(cliente) {
  const historicoDelCliente = baseDatos.buscar(cliente);
  return historicoDelCliente.estaActivo();
}
```
---


## Los nombres de las funciones deberían decir lo que hacen

Las funciones tienen que tener un nombre descriptivo ya puede llevar a confusion nombres como "function1" y resta tiempo.


Mal uso:

```
function añadirAFecha(fecha, mes) {
  // ...
}

const fecha = new Date();

// Es difícil saber que se le está añadiendo a la fecha en este caso
añadirAFecha(fecha, 1);
```

Buen uso:

```
function añadirMesAFecha(mes, fecha) {
  // ...
}

const fecha = new Date();
añadirMesAFecha(1, fecha);
```
---


## Las funciones deberían ser únicamente de un nivel de abstracción

En una funcion es mas importante saber "que hace" en vez de "como lo hace".


Mal uso:

```
function analizarMejorAlternativaJavascript(codigo) {
  const EXPRESIONES_REGULARES = [
    // ...
  ];

  const declaraciones = codigo.split(" ");
  const tokens = [];
  EXPRESIONES_REGULARES.forEach(EXPRESION_REGULAR => {
    declaraciones.forEach(declaracion => {
      // ...
    });
  });

  const ast = [];
  tokens.forEach(token => {
    // lex...
  });

  ast.forEach(nodo => {
    // parse...
  });
}
```

Buen uso:

```
function analizarMejorAlternativaJavascript(codigo) {
  const tokens = tokenize(codigo);
  const ast = lexer(tokens);
  ast.forEach(nodo => {
    // parse...
  });
}

function tokenize(codigo) {
  const EXPRESIONES_REGULARES = [
    // ...
  ];

  const declaraciones = codigo.split(" ");
  const tokens = [];
  EXPRESIONES_REGULARES.forEach(EXPRESION_REGULAR => {
    declaraciones.forEach(declaracion => {
      tokens.push(/* ... */);
    });
  });

  return tokens;
}

function lexer(tokens) {
  const ast = [];
  tokens.forEach(token => {
    ast.push(/* ... */);
  });

  return ast;
}
```
---

## Elimina código duplicado

El eliminar codigo duplicado no solo conlleva una mejora en el rendimiento y en la reduccion de codigo si no que es mas facil leer el codigo


Mal uso:

```
function mostrarListaDesarrolladores(desarrolladores) {
  desarrolladores.forEach(desarrollador => {
    const salarioEsperado = desarrollador.calcularSalarioEsperado();
    const experiencia = desarrollador.conseguirExperiencia();
    const enlaceGithub = desarrollador.conseguirEnlaceGithub();
    const datos = {
      salarioEsperado,
      experiencia,
      enlaceGithub
    };

    render(datos);
  });
}

function mostrarListaJefes(jefes) {
  jefes.forEach(jefe => {
    const salarioEsperado = desarrollador.calcularSalarioEsperado();
    const experiencia = desarrollador.conseguirExperiencia();
    const experienciaLaboral = jefe.conseguirProyectosMBA();
    const data = {
      salarioEsperado,
      experiencia,
      experienciaLaboral
    };

    render(data);
  });
}
```

Buen uso:

```
function mostrarListaEmpleados(empleados) {
  empleados.forEach(empleado => {
    const salarioEsperado = empleado.calcularSalarioEsperado();
    const experiencia = empleado.conseguirExperiencia();

    const datos = {
      salarioEsperado,
      experiencia
    };

    switch (empleado.tipo) {
      case "jefe":
        datos.portafolio = empleado.conseguirProyectosMBA();
        break;
      case "desarrollador":
        datos.enlaceGithub = empleado.conseguirEnlaceGithub();
        break;
    }

    render(datos);
  });
}
```
---


## Asigna objetos por defecto con Object.assign

Object assign sirve para copia todas las propiedades enumerables de uno o más objetos fuente a un objeto destino. Devuelve el objeto destino.


Mal uso:

```
const configuracionMenu = {
  titulo: null,
  contenido: "Bar",
  textoBoton: null,
  cancelable: true
};

function crearMenu(config) {
  config.titulo = config.titulo || "Foo";
  config.contenido = config.contenido || "Bar";
  config.textoBoton = config.textoBoton || "Baz";
  config.cancelable =
    config.cancelable !== undefined ? config.cancelable : true;
}

crearMenu(configuracionMenu);
```

Buen uso:

```
const configuracionMenu = {
  titulo: "Order",
  // El usuario no incluyó la clave 'contenido'
  textoBoton: "Send",
  cancelable: true
};

function crearMenu(configuracion) {
  configuracion = Object.assign(
    {
      titulo: "Foo",
      contenido: "Bar",
      textoBoton: "Baz",
      cancelable: true
    },
    configuracion
  );

  // configuracion ahora es igual a: {titulo: "Order", contenido: "Bar", textoBoton: "Send", cancelable: true}
  // ...
}

crearMenu(configuracionMenu);
```
---


## No utilices banderas o flags

Las banderas o flags te indican de que esa función hace más de una cosa.


Mal uso:

```
function crearFichero(nombre, temporal) {
  if (temporal) {
    fs.create(`./temporal/${nombre}`);
  } else {
    fs.create(nombre);
  }
}
```

Buen uso:

```
function crearFichero(nombre) {
  fs.create(nombre);
}

function crearFicheroTemporal(nombre) {
  crearFichero(`./temporal/${nombre}`);
}
```
---

## Evita los efectos secundarios (parte 1)
 
Una función produce un efecto adverso/colateral si hace otra cosa que recibir un parámetro de entrada y retornar otro valor o valores.


Mal uso:

```
let nombre = 'Ryan McDermott';

function separarEnNombreYApellido() {
  nombre = nombre.split(' ');
}

separarEnNombreYApellido();

console.log(nombre); // ['Ryan', 'McDermott'];
```

Buen uso:

```
function separarEnNombreYApellido(nombre) {
  return nombre.split(' ');
}

const nombre = 'Ryan McDermott';
const nuevoNombre = separarEnNombreYApellido(nombre);

console.log(nombre); // 'Ryan McDermott';
console.log(nuevoNombre); // ['Ryan', 'McDermott'];

```
---


## Evita los efectos secundarios (parte 2)

¡La mayoría de las cosas se pueden refactorizar para que no tengan efectos secundarios! Clonar objetos grandes puede ser muy costosa en términos de rendimiento. Por suerte,hay buenas librerías que permiten este tipo de enfoque de programación. Es rápido y no requiere tanta memoria como te costaría a ti clonar manualmente los arrays y los objetos.


Mal uso:

```
const añadirObjetoAlCarrito = (carrito, objeto) => {
  carrito.push({ objeto, fecha: Date.now() });
};
```

Buen uso:

```
const añadirObjetoAlCarrito = (carrito, objeto) => {
  return [...carrito, { objeto, fecha: Date.now() }];
};
```
---

## No escribas en variables globales

La contaminación global es una mala práctica en JavaScript porque podría chocar con otra librería y usuarios de tu API no serían conscientes de ello hasta que tuviesen un error en producción.


Mal uso:

```
Array.prototype.diff = function diff(matrizDeComparación) {
  const hash = new Set(matrizDeComparación);
  return this.filter(elemento => !hash.has(elemento));
};
```

Buen uso:

```
class SuperArray extends Array {
  diff(matrizDeComparación) {
    const hash = new Set(matrizDeComparación);
    return this.filter(elemento => !hash.has(elemento));
  }
}
```
---


## Da prioridad a la programación funcional en vez de la programación imperativa

Javascript no es un lenguage funcional en la misma medida que lo es Haskell, pero tiene aspectos que lo favorecen. Los lenguages funcionales pueden ser más fáciles y limpios de testear.


Mal uso:

```
const datosSalidaProgramadores = [
  {
    nombre: "Uncle Bobby",
    liniasDeCodigo: 500
  },
  {
    nombre: "Suzie Q",
    liniasDeCodigo: 1500
  },
  {
    nombre: "Jimmy Gosling",
    liniasDeCodigo: 150
  },
  {
    nombre: "Gracie Hopper",
    liniasDeCodigo: 1000
  }
];

let salidaFinal = 0;

for (let i = 0; i < datosSalidaProgramadores.length; i++) {
  salidaFinal += datosSalidaProgramadores[i].liniasDeCodigo;
}
```

Buen uso:

```
const datosSalidaProgramadores = [
  {
    nombre: "Uncle Bobby",
    liniasDeCodigo: 500
  },
  {
    nombre: "Suzie Q",
    liniasDeCodigo: 1500
  },
  {
    nombre: "Jimmy Gosling",
    liniasDeCodigo: 150
  },
  {
    nombre: "Gracie Hopper",
    liniasDeCodigo: 1000
  }
];

const salidaFinal = datosSalidaProgramadores
  .map(salida => salida.linesOfCode)
  .reduce((totalLinias, linias) => totalLinias + linias);
```
---

## Encapsula los condicionales

Intentar no tener condiciones sueltas tales como un if sueltos en el codigo


Mal uso:

```
if (fsm.state === "cogiendoDatos" && estaVacio(listaNodos)) {
  // ...
}
```

Buen uso:

```
function deberiaMostrarSpinner(fsm, listaNodos) {
  return fsm.state === "cogiendoDatos" && estaVacio(listaNodos);
}

if (deberiaMostrarSpinner(fsmInstance, listNodeInstance)) {
  // ...
}
```
---








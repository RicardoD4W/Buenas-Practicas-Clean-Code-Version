# SOLID

* [Principio de Responsabilidad Única(SRP)](#SRP)
* [Principio de abierto/cerrado (OCP)](#OCP)
* [Principio de sustitución de Liskov (LSP)](#LSP)
* [Principio de segregación de la interfaz (ISP)](#ISP)
* [Principio de inversión de la dependencia (DIP)](#DIP)



## SRP
El primer principio de SOLID llamado Principio de Responsabilidad Única indica que una clase debería ser responsable de una única funcionalidad. En otras palabras, la clase solo debería tener una única razón para cambiar.


### Beneficios del principio de responsabilidad única:

```

  1. En relación al testing. Se simplifica 
        porque una clase tiene una única responsabilidad... 

  2. Se disminuye el acoplamiento pirque menor funcionalidad 
        en una clase hará que esta tenga menos dependencias. 
        
  3. La organización de las clases y los paquetes 
        será mejor y más sencillo.

```




### Mal uso

```java

package solid;

class UserLogin {

    private final DataBase db;

    UserLogin(DataBase db){
      this.db = db;
    }

    void login (String userName, String password) {
      User user = db.findUserByUserName(userName);
      if (user == null){
        //do something
      }
      //login process
    }

    void sendMail (User user, String msg){
      //send email to user
    }


}

```

\
Esta clase UserLogin tiene como responsabilidad realizar el proceso de login pero además le dimos la responsabilidad de de enviar mensajes al usuario.
Este código viola el principio de responsabilidad unica. Está haciendo dos cosas con objetivos diferentes.


### Buen uso

```java

package solid;

class EmailSender {

    void sendMail (User user, String msg){
      //send email to user
    }

}

```

\
¿Entonces qué deberíamos hacer?

Sería conveniente separar la clase en dos. Una para lo específico del login y otra para la funcionalidad de envío de mensajes.


## OCP  
El Principio de Abierto-Cerrado, del inglés "The Open-Close Principle (OCP)", nos viene a decir que cualquier entidad software (clases, módulos, funciones, etc.) debe de estar abierta para ser extendida en funcionalidad pero cerrada para ser modificada. Es decir, una clase que cumpla con OCP tiene estas dos características:


```

  1. La funcionalidad del módulo puede cambiarse o extenderse
                en base a los cambios que requiera el sistema.

  2. Extender la funcionalidad de un módulo no implica
        cambios en el código fuente de ese módulo en sí mismo.

```


\
![Ejemplo coche](./imgS/ejemploCoche.png)

En este caso, la interfaz [IConductor] es la abstracción que define la clase [Conductor] para conducir un [Vehículo]. Observa que la interfaz se llama [IConductor]en lugar de IVehículo porque el que define la funcionalidad es el [Conductor] mientras que [Vehículo] es únicamente una implementación de esa interfaz. Para implementar el cambio que restringe que un [Conductor] sólo puede conducir vehículos a motor bastaría únicamente con cambiar la implementación de [Vehículo] para justarse a las nuevas necesidades.

Con este diseño, la clase [Conductor] cumple con OCP, pues está abierta a cambios (respecto a conducir vehículos) y cerrado a los cambios (para cambiar el comportamiento de los vehículos, no se necesita cambiar el comportamiento del conductor).Otro tema sería que los cambios que se pidieran no fuesen soportados por la interfaz disponible. Por ejemplo, tener en cuenta vehículos voladores. En este caso los cambios serían a nivel de requerimientos de más alto nivel, por lo que se entiende que no quede más remedio que cambiar la clase [Conductor], la interfaz [IConductor], y evidentemente todas las implementaciones de esta interfa










## LSP
El principio de sustitución de Liskov nos dice que si en alguna parte de nuestro código estamos usando una clase, y esta clase es extendida, tenemos que poder utilizar cualquiera de las clases hijas y que el programa siga siendo válido.


```

  1. Esto nos obliga a asegurarnos de que cuando extendemos 
               una clase no estamos alterando el comportamiento de la padre.

  2. Este principio viene a desmentir la idea preconcebida de
               que las clases son una forma directa de modelar la realidad, y que
               hay que tener cuidado con esa modelización.

```


\
![Ejemplo LSP](./imgS/image001.png)

Este es un ejemplo de LSP ya que deberíamos poder cambiar las clases [Vehículo], por sus hijas sin que se den errores y problemas.



\
![Ejemplo LSP](./imgS/ejemploLSPbien.png)
Este es un ejemplo de LSP bien hecho ya que podemos cambiar la  [Operacion] a placer sin que se den errores, un mal ejemplo habría sido uno donde en vez de tener "Operador1" y "Operador2" tendría funciones como "suma" o "resta".






## ISP
El principio nos indica que una clase debe de implementar únicamente las interfaces que necesita, es decir, que no necesite tener que implementar métodos que no utilice. Se aplica a una interfaz amplia y compleja para escindirla en otras más pequeñas y específicas, de tal forma que cada cliente use solo aquella que necesite.

Imaginemos que tenemos un negocio de venta de ordenadores de escritorio, sabemos que todas las ordenadores deberían de extender de la clase Ordenador y tendríamos algo como esto:



```js

class Ordenador {
  marca;
  modelo;

  constructor(marca, modelo) {
    this.marca = marca;
    this.modelo = modelo;
  }

  obtenerMarca() {
    return this.marca;
  }

  obtenerModelo() {
    return this.modelo;
  }

  guardarMarca(marca) {
    this.marca = marca;
  }

  guardarModelo(modelo) {
    this.modelo = modelo;
  }
}

class Portatil extends Ordenador {
   ...
}

```

En nuestro negocio todo va de maravilla y ahora queremos extender un poco más nuestro catalogo de productos, así que decidimos optar por empezar a vender ordenadores portátiles. Un atributo útil de un portátil es el tamaño de la pantalla integrada, pero como bien sabemos esto solo esta presente en los portátiles y no ordenadores de escritorio (generalizando), podemos hacer esto:

```js

  class Ordenador {
  marca;
  modelo;

  constructor(marca, modelo) {
    this.marca = marca;
    this.modelo = modelo;
  }

  obtenerMarca() {
    return this.marca;
  }

  obtenerModelo() {
    return this.modelo;
  }

  guardarMarca(marca) {
    this.marca = marca;
  }

  guardarModelo(modelo) {
    this.modelo = modelo;
  }
}

const Portatil = (clasePadre) => {
  return (
    class extends clasePadre {
      constructor(marca, modelo){
        super(marca, modelo);
      }

      guardarTamanioPantalla(tamanio) {
        this.tamanio = tamanio;
      }

      obtenerTamanioPantalla() {
        return this.tamanio;
      }

    }
  )
}

```

## DIP
En este principio se establecen que las dependencias deben de estar en las abstracciones y no en las concreciones, en otras palabras, nos piden que las clases nunca dependan de otras clases y que toda esta relación debe estar en una abstracción. Este principio tiene dos reglas:


```

  1. Los módulos de alto nivel no deben de depender de módulos de bajo nivel. Esta lógica debe de estar en una abstracción.

  2. Las abstracciones no deben de depender de detalles. Los detalles deberían depender de abstracciones. 

```


  
Imagina que tenemos una clase que nos permite enviar un correo:


```js

  class Correo {
  provider;

  constructor() {
    // Levantar una instancia de google mail, este código es con fin de demostración.
    this.provider = gmail.api.createService();
  }

  enviar(mensaje) {
    this.provider.send(mensaje);
  }
}

var correo = new Correo();
correo.enviar('hola!');

```
\
En este ejemplo se puede ver que se está rompiendo la regla, puesto que la clase correo depende del proveedor de servicio, ¿qué pasaría si después queremos usar Yahoo y no Gmail?

Para solucionar esto debemos eliminar esa dependencia y añadirla como una abstracción.

```js

  class GmailProveedor {
  constructor() {
    // Levantar una instancia de google mail, este código es con fin de demostración.
    this.provider = gmail.api.createService();
  }
  enviar(mensaje) {
    this.provider.sendAsText(mensaje);
  }
}
class Correo {
  constructor(proveedor) {
    this.proveedor = proveedor;
  }
  enviar(mensaje) {
    this.proveedor.send(mensaje);
  }
}
var gmail = new GmailProveedor();
var correo = new Correo(gmail);
correo.enviar('hola!');

```

De esta forma ya no nos importa el proveedor ni la forma en que implementa el envío de correos el proveedor, la clase de Correo solo se ocupa de una única cosa, pedirle al proveedor que envíe un correo.








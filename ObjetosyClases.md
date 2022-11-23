# OBJETOS Y ESTRUCTURAS DE DATOS 
## Utiliza getters y setters

 Usar getters y setters para acceder a la información del objeto está mejor que simplemente accediendo a esa propiedad del objeto. ¿Por qué?
    - Si quieres modificar una propiedad de un objeto, no tienes que ir mirando si existe o no existe para seguir mirando a niveles más profundos del objeto.
    - Encapsula la representación interna (en caso de tener que comprobar cosas, mirar en varios sitios...)
    - Es sencillo añadir mensajes y manejos de error cuando hacemos get y set
    - Te permite poder hacer lazy load en caso de que los datos se recojan de una Base de Datos (bbdd)

MAL

```javascript
function newUser_Mal(){
    return {
        name: "",
        age: 0,
    }
}

let user_mal = newUser_Mal()
user_mal.name = "Alejandro Torres Castillo"
user_mal.age = 22
```
BIEN

```javascript
function newUser_Bien(){
    let name = ""
    let age = 0

    let getName = () => name
    let setName = (name) => this.name = name
    let getAge = () => age
    let setAge = (age) => this.age = age

    return{
        getName, setName,
        getAge,  setAge
    }
}

let user_bien = newUser_Bien()
user_bien.setName("Alejandro Torres Castillo")
user_bien.setAge(22)
```

## Hacer que los objetos tengan atributos/métodos privados

Esto se puede hacer mediante clojures (de ES5 en adelante). 

MAL
```javascript 
const EMPLOYEE = (name) => this.name = name

EMPLOYEE.prototype.getName = function getName() { 
    return this.name 
}

const  employee_mal = new EMPLOYEE("Alfredo")
console.log(employee_mal.getName()) // Alfredo
delete employee_mal.name
console.log(employee_mal.getName()) // undefinde
```

BIEN
```javascript
function createEmployee(name){
    return {
        getName(){
            return name;
        }
    }
}

const  employee_bien = createEmployee("Alfredo")
console.log(employee_bien.getName()) // Alfredo
delete employee_bien.name
console.log(employee_bien.getName()) // Alfredo
```
# CLASES
## Añadir las propiedades/funciones de una clase al crearla
Es muy complicado de conseguir que un código sea entendible y fácil 
de leer con herencia de clases, construcción y metodos típicos de clases
con las clases de ES5. Si necesitas herencia (y de seguro, que no la necesitas)
entonces, dale prioridad a las clases ES2015/ES6. De todas las maneras, 
deberías preferir pequeñas funciones antes que ponerte a hacer clases. 
Solo cuando tengas un código largo o cuando veas necesaria la implementación de clases, añádelas.

MAL
```javascript
const Animal = function(patas){
    if(!(this instaceof Animal)) throw new Error("Inicializa Animal con `new`");

    this.patas = patas;
};

Animal.prototype.andar = function andar() {};
```

BIEN
```javascript
class Animal {
    constructor(patas){
        this.patas = patas;
    }

    andar(){
        /* ... */
    }
}
```

## Si no devuelve nada la función, devolver el mismo objeto
Este es un patrón útil en Javascript y verás que muchas librerías
como jQuery o Lodash lo usan. Permite que tu código sea expresivo
y menos verboso. Por esa razón, utiliza las funciones anidadas y 
date cuenta de que tan limpio estará tu código. En las funciones 
de tu clase, sencillamente retorna this al final de cada una y con
eso, tienes todo lo necesario pra poder anidar las llamadas a las funciones.

MAL
```javascript
class Churreria {
    constructor(localidad, logotipo){
        this.localidad = localidad;
        this.logotipo = logotipo;
    }

    cambiarLugar(localidad){
        this.localidad = localidad;
    }

    cambiarLogo(logotipo){
        this.logotipo = logotipo;
    }
}

let churreria = new Churreria("Martos", "El café bien negro");
churreria.cambiarLogo("Siempre entra");
churreria.cambiarLugar("TorredelCampo");
```

BIEN
```javascript
class Churreria {
    constructor(localidad, logotipo){
        this.localidad = localidad;
        this.logotipo = logotipo;
    }

    cambiarLugar(localidad){
        this.localidad = localidad;
        return this;
    }

    cambiarLogo(logotipo){
        this.logotipo = logotipo;
        return this;
    }
}

let churreria = new Churreria("Martos", "El café bien negro");
churreria.cambiarLogo("Unos cuantos entran solo a comer").cambiarLugar("Rute");
```

## Prioriza la composición en vez de la herecia
Como se citó en Patrones de Diseño por "the Gang of Four", deberías priorizar la composición en vez de la herecia siempre que puedas. Hay muy buenas razones para usar tanto la herecia como la composición. El problema principal es que nuestra mente siempre tiende a la herencia como primera opción, pero deberíamos de pensar qué tan bien nos encaja la composición en ese caso particular porque en muchas ocasiones es lo más acertado.

Te estarás preguntando entonces, ¿Cuando debería yo usala herencia? Todo depende. Depende del problema que 
tengas entre mano, pero ya hay ocasiones particularedonde la herencia tiene más sentido que la composición:
- Tu herencia representa una relación "es un/a" en vez de "tiene un/a" 
(Humano->Animal vs. Usuario->DetallesUsuario)
- Puedes reutilizar código desde las clases base 
(Los humanos pueden moverse como animales)
- Quieres hacer cambios generales a clases derivadacambiando la clase base. 
(Cambiar el consumo de calorías a todos los animales mientras se mueven)

MAL
```javascript 
class Rueda {
    constructor(diametro, desgaste) {
        this.diametro = diametro
        this.desgaste = desgaste    
    }
    rodar = () => this.degaste++
}

// Mal porque un Coche no tiene los mismos atributos que la Rueda
class Coche extends Rueda {
    constructor(motor, km) {
        super();
        this.motor = motor;
        this.km = km;
    }
} 
```
BIEN
```javascript 
// Sin modificar la clase rueda la usamos con agregacion y sin recurrir a la herencia 
class Coche{

    constructor(motor, km) {
        this.motor = motor;
        this.km = km;
        this.ruedas = []
    }
    
    cambiarRuedas = function(index, diametro, desgaste){
        this.ruedas[index] = new Rueda(diametro, desgaste)
    }
}
```
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
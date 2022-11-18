# Manejo de errores

## 1. No ignores los errores capturados:

El uso de try/catch hace que tengas que elaborar un plan de reacción a aquellos errores y no ignorarlos con un simple console.log(), que no aporta ninguna solución.


Mal uso:
```javascript
try{
    lanzaError();
}catch(error){
    console.log(error);
}
```

Buen uso:
```javascript
try{
    lanzaError();
}catch(error){
    // Console.error es más apropiado para mostrar un error que el Console.log
    console.error(error);
    // Para hacer más real la visibilidad del error
    informarAlUsuario(mensaje, error);
}
```

---

## 2. No ignores las promesas rechazadas:

Las promesas encadenadas son excelentes manejando errores. Cuando una promesa es rechazada, el control salta al manejador de rechazos más cercano. Por eso no es conveniente ignorarlas.

Mal uso:
```javascript
obtenerInformacion()
    .then(info => {
        lanzaError(info);
    })
    .catch(error => {
        alert(error);
    });
```

Buen uso:
```javascript
obtenerInformacion()
    .then(info => {
        lanzaError(info);
    })
    .catch(error => {
        console.error(error);
        informarAlUsuario(error);
    });
```
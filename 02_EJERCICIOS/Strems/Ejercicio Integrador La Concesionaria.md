---
Dificultad: Difícil
Tipo: Streams
---
# 🚗 Ejercicio Integrador: La Concesionaria

## 🚀 Enunciado:
Una casa de venta de vehículos desea crear una aplicación para gestionar los autos que tiene a la venta. Para ello necesita (de cada auto) los siguientes datos: `marca`, `modelo` y `costo`.

A partir de la lista de datos proporcionada, logra que el programa pueda:
1. Ordenar la lista de vehículos por **precio de menor a mayor** e imprimir por pantalla el resultado.
2. Ordenar al mismo tiempo tanto por **marca** como por **precio** (ambos criterios) e imprimir el resultado por pantalla.
3. Extraer una lista de todos los vehículos cuyo precio **no supere** los 23000.
4. Filtrar únicamente los vehículos de marca **Chevrolet** y **Volkswagen**.
5. Mostrar todos los autos cuyo modelo **contenga** por lo menos una letra "a".

### 📋 Datos iniciales:

```java
// Lista base para trabajar
List<Vehiculo> inventario = List.of(
    new Vehiculo("Volkswagen", "Amarok", 25000.0),
    new Vehiculo("Volkswagen", "Taos", 32000.0),
    new Vehiculo("Chevrolet", "Onix", 22000.0),
    new Vehiculo("Chevrolet", "Tracker", 30000.0),
    new Vehiculo("Fiat", "Cronos", 21000.0),
    new Vehiculo("Fiat", "Pulse", 24000.0),
    new Vehiculo("Toyota", "Corolla", 28000.0),
    new Vehiculo("Toyota", "Yaris", 23000.0),
    new Vehiculo("Renault", "Stepway", 20000.0),
    new Vehiculo("Renault", "Duster", 27000.0),
    new Vehiculo("Nissan", "Versa", 25000.0)
);
````

> [!NOTE] Nota
> 
> - Primero deberás crear la clase `Vehiculo` con sus atributos, constructor, _getters_ y sobreescribir el método `toString()` para que al imprimir los objetos se lean correctamente en la consola.
>     
> - Para el **Punto 2**, investiga cómo encadenar comparadores en la API de Java. ¡Existe un método muy útil llamado `.thenComparing()`!
>     
> - Para el **Punto 5**, asegúrate de que tu filtro sea insensible a mayúsculas y minúsculas para que no se te escape la "Amarok".
>

# Introducción a la API de Streams

La API de Streams nos permite procesar colecciones de datos de forma declarativa. En lugar de decirle a Java *cómo* hacer cada paso con bucles y condicionales, le decimos *qué* queremos obtener.

> [!IMPORTANT] Regla Universal
> Los Streams se pueden usar en **cualquier colección** de Java (`ArrayList`, `LinkedList`, `HashSet`, etc.). Solo tienes que llamar al método `.stream()` sobre tu colección original para iniciar la cinta transportadora.


---

## El Contraste: Estructurado vs Funcional

Imagina que tenemos una lista de números y queremos obtener **solo los números pares que sean mayores a 10, y multiplicarlos por 2**.

### El pasado (Programación Estructurada / Imperativa)
Lleno de variables temporales, bucles `for` anidados y condicionales `if`. Es fácil perder el hilo de lo que hace el código si crece mucho.

```java
List<Integer> numeros = List.of(5, 12, 8, 20, 15, 3);
List<Integer> resultado = new ArrayList<>();

for (Integer numero : numeros) {
    if (numero % 2 == 0) { // 1. Verificamos si es par
        if (numero > 10) { // 2. Verificamos si es mayor a 10
            resultado.add(numero * 2); // 3. Lo multiplicamos y guardamos
        }
    }
}

System.out.println(resultado); // Imprime: [24, 40]
````

### El presente (Programación Funcional con Streams)

El código es limpio, directo y se lee de arriba hacia abajo como si fuera una tubería por la que pasa el agua.

```java
List<Integer> numeros = List.of(5, 12, 8, 20, 15, 3);

List<Integer> resultado = numeros.stream() // Abrimos la llave del agua
    .filter(n -> n % 2 == 0)               // 1. Filtramos los pares (Predicate)
    .filter(n -> n > 10)                   // 2. Filtramos los mayores a 10 (Predicate)
    .map(n -> n * 2)                       // 3. Transformamos (Function)
    .toList();                             // 4. Empacamos en una lista nueva (Terminal)

System.out.println(resultado); // Imprime: [24, 40]
```

## El Catálogo de Operaciones

> [!NOTE] Un mundo de posibilidades 
> Es vital recalcar que existen **muchísimos** métodos intermediarios y finales en la API de Java. Aquí veremos los más utilizados en el día a día para entender la lógica, pero ten en cuenta que la caja de herramientas es inmensa y siempre hay un método para lo que necesites.

### 1. Operaciones Intermedias (La Maquinaria)

Recuerda: son **perezosas**. Devuelven un nuevo Stream para que puedas seguir encadenando más operaciones, pero no procesan ni mueven un solo dato hasta que no haya una operación terminal al final.

- **`.filter(Predicate)`**: Deja pasar solo los elementos que cumplen una condición (`true`).
    
- **`.map(Function)`**: Transforma cada elemento en otra cosa (ej. extraer solo los nombres de una lista de objetos `Persona`).
    
- **`.sorted()`**: Ordena los elementos que van pasando.
    
- **`.distinct()`**: Elimina los elementos duplicados (deja pasar solo copias únicas).
    
- **`.limit(long)`**: Deja pasar solo los primeros _N_ elementos y luego cierra la compuerta.
    

**Ejemplo combinando intermedias:**

```Java
List<String> nombres = List.of("Ana", "Juan", "Pedro", "Ana", "Luis");

nombres.stream()
       .distinct()          // Quita la "Ana" duplicada
       .sorted()            // Ordena alfabéticamente: Ana, Juan, Luis, Pedro
       .limit(2)            // Se queda solo con los primeros 2: Ana, Juan
       // (Falta la operación terminal para que se ejecute realmente)
```

### 2. Operaciones Terminales (El Botón de Encendido)

Estas consumen el Stream. Cierran la tubería, encienden la maquinaria y devuelven un resultado real (una lista, un número, un booleano, o nada). **Un Stream no se puede volver a usar después de una operación terminal.**

- **`.toList()` / `.collect(Collectors.toList())`**: Empaca los elementos sobrevivientes en una nueva Lista.
    
- **`.forEach(Consumer)`**: Ejecuta una acción (como imprimir) por cada elemento que llega al final.
    
- **`.count()`**: Devuelve un `long` con la cantidad total de elementos que lograron llegar al final del recorrido.
    
- **`.anyMatch(Predicate)`**: Devuelve un `boolean` rápido. Si _al menos un_ elemento cumple la condición, detiene el proceso y devuelve `true`.
    
- **`.reduce(BinaryOperator)`**: Combina todos los elementos en un solo resultado (ej. sumar todos los números, o concatenar todos los textos).
    

**Ejemplos con terminales:**

```Java
List<Integer> edades = List.of(15, 22, 17, 30);

// Terminal: count() -> Queremos saber cuántos son mayores de edad
long cantidadMayores = edades.stream()
                             .filter(e -> e >= 18)
                             .count(); 
// Resultado: 2

// Terminal: anyMatch() -> Queremos saber si hay alguien de exactamente 30 años
boolean hayAlguienDe30 = edades.stream()
                               .anyMatch(e -> e == 30); 
```
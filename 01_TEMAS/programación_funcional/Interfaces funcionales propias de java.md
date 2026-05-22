---
Tipo: PF
Tema: Funciones lambdas
---
Si aún no ha leído la nota sobre las funciones lambdas le recomiendo leerla [[Funciones lambdas| presione este enlace]]
# Interfaces Funcionales Integradas (java.util.function)

Para evitar que tengamos que crear las mismas interfaces una y otra vez (como `Mensajero` u `OperacionMatematica`), Java introdujo un paquete con interfaces "prefabricadas", con el objetivo de no tener que crear multiples interfaces para lograr usar expresiones lambdas.

Estas se dividen en 4 familias principales, más sus variantes `Bi` (que aceptan dos parámetros en lugar de uno).

---
## 1. Consumer<T> (El Consumidor)
**Consume un dato, pero no devuelve nada.**

* **Qué recibe:** 1 parámetro (`T`).
* **Qué devuelve:** Nada (`void`).
* **Método que ejecuta:** `.accept(T)`
* **Caso de uso típico:** Imprimir por consola, guardar en base de datos, modificar el estado de un objeto.
>[!example] Ejemplo
>```java
>import java.util.function.Consumer;
>
>// Declaración
>Consumer<String> saludar = nombre -> System.out.println("Hola, " + nombre);
>
>// Uso manual
>saludar.accept("Angely"); 
>
>// Uso en la vida real (Listas)
>List<String> nombres = List.of("Ana", "Juan");
>nombres.forEach(nombre -> System.out.println("Hola, " + nombre));


## 2. Supplier (El Proveedor)

**No recibe nada, pero siempre te entrega un dato nuevo.**

- **Qué recibe:** Nada `()`.
    
- **Qué devuelve:** 1 resultado (`T`).
    
- **Método que ejecuta:** `.get()`
    
- **Caso de uso típico:** Generar números aleatorios, crear instancias por defecto, obtener fechas actuales.
    
>[!example] ejemplo
>```java
>import java.util.function.Supplier;
>
>// Declaración
>Supplier<Double> numeroAleatorio = () -> Math.random();
>
>// Uso manual
>System.out.println(numeroAleatorio.get()); 
>

## 3. Predicate (El Evaluador)

**Evalúa una condición y te dice si es verdadera o falsa.**

- **Qué recibe:** 1 parámetro (`T`).
    
- **Qué devuelve:** `boolean`.
    
- **Método que ejecuta:** `.test(T)`
    
- **Caso de uso típico:** Filtrar listas, validar datos (ej. contraseñas), comprobar si un número es par.


>[!example] Ejemplo
>```java
>import java.util.function.Predicate;
>// Declaración
>Predicate<Integer> esMayorDeEdad = edad -> edad >= 18;
>
>// Uso manual
>System.out.println(esMayorDeEdad.test(20)); // true
>
>// Uso en la vida real (Filtrado)
>List<Integer> edades = new ArrayList<>(List.of(15, 20, 12));
>edades.removeIf(edad -> edad < 18); // Elimina el 15 y el 12


## 4. Function<T, R> (El Transformador)

**Recibe un tipo de dato y lo transforma en otro.**

- **Qué recibe:** 1 parámetro de entrada (`T`).
    
- **Qué devuelve:** 1 resultado de salida (`R`).
    
- **Método que ejecuta:** `.apply(T)`
    
- **Caso de uso típico:** Recibir un String y devolver su tamaño en Integer, extraer el ID de un objeto completo.
    


>[!example] Ejemplo
>```Java
>import java.util.function.Function;
>
>// Declaración: Recibe String, devuelve Integer
>Function<String, Integer> contarLetras = texto -> texto.length();
>
>// Uso manual
>int cantidad = contarLetras.apply("Programación"); // Devuelve 12


## 5. La variante Bi: BiConsumer<T, U>

Casi todas las interfaces anteriores tienen una versión `Bi` (Bidireccional) cuando necesitas pasarle **dos parámetros** en lugar de uno.

El más común es el `BiConsumer`.

- **Qué recibe:** 2 parámetros de tipos distintos (`T` y `U`).
    
- **Qué devuelve:** Nada (`void`).
    
- **Método que ejecuta:** `.accept(T, U)`
    


>[!example] Ejemplo
>```java
>import java.util.function.BiConsumer;
>
>// Declaración: Recibe un String (nombre) y un Integer (edad)
>BiConsumer<String, Integer> msjPersonalizado = (nombre, edad) -> {
>	System.out.println("Usuario: " + nombre + " | Edad: " + edad);
>};
>// Uso manual
>msjPersonalizado.accept("Carlos", 28);
>// Uso en la vida real (Recorrer un HashMap o Diccionario)
>Map<String, Integer> usuarios = Map.of("Ana", 25, "Juan", 30);
>usuarios.forEach((clave, valor) -> System.out.println(clave + " tiene " + valor + " años"));


> [!TIP] El truco para recordarlas
> 
> - Si **entra** algo y **no sale** nada = `Consumer`
>     
> - Si **no entra** nada y **sale** algo = `Supplier`
>     
> - Si **entra** algo y sale un **boolean** = `Predicate`
>     
> - Si **entra** algo y sale **otra cosa transformada** = `Function`
>
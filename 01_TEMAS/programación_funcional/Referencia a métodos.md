
# Referencia a Métodos

## ¿Qué es y por qué existe?
La **Referencia a Métodos** es un atajo sintáctico (una forma más corta de escribir) para una expresión lambda. 

Se utiliza **exclusivamente** cuando tu lambda no hace ninguna lógica nueva, sino que su único propósito es **llamar a un método que ya existe**. El operador que se utiliza son los dos puntos dobles: `::`.

> [!INFO] La analogía de la tarjeta de presentación
> Imagina que alguien te pide el número de un fontanero. 
> * **La Lambda:** Es escribir el número del fontanero en un papel en blanco y dárselo. `() -> llamarAlFontanero()`
> * **La Referencia a Método:** Es simplemente entregarle la tarjeta de presentación del fontanero. `Fontanero::llamar`
> Ambas logran lo mismo, pero la segunda es más directa.

---
## La Regla de Oro
Para poder usar `::`, los parámetros que recibe la lambda deben **coincidir exactamente** (en cantidad y tipo) con los parámetros que requiere el método que estás llamando. Si necesitas modificar el dato antes de pasarlo, **no** puedes usar referencias a métodos; debes usar una lambda normal.

---

## Los 4 Tipos de Referencias a Métodos

Este tema suele confundir porque el operador `::` se comporta ligeramente distinto dependiendo de *a qué* le estés haciendo referencia. Vamos uno por uno.

### 1. Referencia a un Método Estático
Es el más fácil de entender. Llamas a un método que pertenece a una clase directamente.
* **Sintaxis:** `Clase::metodoEstatico`

```java
// Tenemos una lista de números en texto
List<String> numerosTexto = List.of("1", "2", "3");

// VERSIÓN LAMBDA: 
// Recibe un String 'n' y se lo pasa a Integer.parseInt()
numerosTexto.stream()
            .map(n -> Integer.parseInt(n));

// VERSIÓN REFERENCIA A MÉTODO:
// Como lo único que hace la lambda es pasar el dato tal cual al método estático...
numerosTexto.stream()
            .map(Integer::parseInt); 
````

### 2. Referencia a un Método de Instancia (De un objeto específico)

Aquí el método no pertenece a una clase global, sino a un **objeto que ya creaste** y que vive en una variable.

- **Sintaxis:** `objetoInstanciado::metodo`
    

```java
// 1. Instanciamos un objeto específico
String prefijo = "Aviso: ";

// VERSIÓN LAMBDA:
// Usamos el objeto 'prefijo' que está fuera de la lambda
Consumer<String> imprimirConAviso = mensaje -> System.out.println(prefijo.concat(mensaje));

// VERSIÓN REFERENCIA A MÉTODO:
// Apuntamos al objeto 'prefijo' y llamamos a su método 'concat'
Consumer<String> imprimirConAvisoRef = prefijo::concat;

// El clásico System.out.println también es de este tipo:
// 'out' es un objeto instanciado de tipo PrintStream que vive dentro de la clase 'System'.
Consumer<String> imprimir = System.out::println;
```

### 3. Referencia a un Método de Instancia (De un objeto arbitrario)

_⚠️ Este es el que más confunde a los estudiantes._

Se usa cuando el método que quieres llamar **pertenece al mismo objeto que estás recibiendo como parámetro**.

- **Sintaxis:** `Clase::metodoInstancia`
    

```Java
// Imagina una clase Persona con un método getNombre()
List<Persona> personas = obtenerPersonas();

// VERSIÓN LAMBDA:
// Recibimos un objeto 'p' y llamamos a UN MÉTODO DE ESE MISMO OBJETO 'p'.
personas.stream()
        .map(p -> p.getNombre());

// VERSIÓN REFERENCIA A MÉTODO:
// Ponemos el nombre de la CLASE (Persona), pero Java es inteligente y sabe 
// que debe ejecutar getNombre() sobre cada objeto individual que va llegando.
personas.stream()
        .map(Persona::getNombre);
```

> [!NOTE] ¿Por qué Persona::getNombre y no p::getNombre?
> 
> Porque en la referencia a método no declaramos variables temporales (como `p`). Le decimos a Java: _"De cualquier objeto de tipo **Persona** que te llegue, aplícale su método **getNombre**"_.

### 4. Referencia a un Constructor

Se usa cuando tu lambda simplemente crea un objeto nuevo usando `new`.

- **Sintaxis:** `Clase::new`
    

```java
// Queremos crear una lista de objetos Persona vacíos
Supplier<Persona> creadorDePersona;

// VERSIÓN LAMBDA:
creadorDePersona = () -> new Persona();

// VERSIÓN REFERENCIA A MÉTODO:
creadorDePersona = Persona::new;

// Ahora cada vez que llamemos a get(), creará un objeto nuevo:
Persona p1 = creadorDePersona.get();
```

## Resumen Visual Rápido

| ***Qué quiero hacer***                 | ***Lambda***                   | ***Referencia a Método*** |
| -------------------------------------- | ------------------------------ | ------------------------- |
| **Llamar método estático**             | **`(x) -> Math.sqrt(x)`**          | `Math::sqrt`              |
| **Llamar método de un objeto**         | **`(x) -> System.out.println(x)`** | `System.out::println`     |
| **Llamar método del propio parámetro** | **`(x) -> x.toUpperCase()`**       | `String::toUpperCase`     |
| **Crear un objeto nuevo**              | **`() -> new ArrayList<>()`**      | `ArrayList::new`          |
- [[Streams | Siguiente tema]] 

>[!note] Nota
>La referencia de métodos al principio es algo confusa, pero no es un concepto que se deba memorizar. Con comprender cómo funciona, saber qué significa `::` y lograr identificar qué tipo de referencia es, es más que suficiente. Tampoco es un concepto que impida aprender Streams u otro tema más importante.
>
>La referencia de métodos es simplemente azúcar sintáctico.

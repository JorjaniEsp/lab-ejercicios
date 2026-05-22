
> [!TIP] El Secreto de los Streams: Entender, no memorizar
> La API de Streams tiene docenas de métodos intermediarios y finales. **No es necesario aprendérselos de memoria.** Lo verdaderamente importante es comprender la lógica del flujo: de dónde vienen los datos, qué transformaciones necesitan y cómo quieres empaquetar el resultado. 
>
> Recuerda que la documentación oficial está a un clic de distancia y la IA puede facilitarte la sintaxis exacta. Tu trabajo como programador es diseñar la lógica; las herramientas te dan el código.

---

# Recetario de Streams: Operaciones Clave y Ejemplos

Los Streams se componen de un **Origen** (la lista), **Operaciones Intermedias** (transforman/filtran y devuelven otro Stream) y una **Operación Terminal** (cierra el flujo y devuelve un resultado).

## 1. Transformación Profunda: `.map(Function)`
**¿Cuándo usarlo?** Cuando necesitas extraer una propiedad específica de un objeto o transformar el tipo de dato que va por la cinta transportadora.
**¿Qué hace?** Recibe un elemento, le aplica una función y lo cambia por otro.

```java
// Escenario: Tenemos una lista de productos para un sistema de cotizaciones
List<Producto> catalogo = List.of(
    new Producto("Plantilla PDF Matemáticas", 5.00),
    new Producto("Sistema de Inventario Excel", 15.00)
);

// Queremos extraer ÚNICAMENTE los nombres de los productos
List<String> nombresProductos = catalogo.stream()
    .map(producto -> producto.getNombre()) // Transformamos de Producto a String
    .toList(); 

System.out.println(nombresProductos); // [Plantilla PDF Matemáticas, Sistema de Inventario Excel]
````

## 2. Empacando el resultado: Devolver otra lista (`.toList()`)

**¿Cuándo usarlo?** Cuando no solo quieres imprimir o calcular algo, sino que necesitas guardar los datos sobrevivientes en una nueva variable para usarlos en el resto de tu programa. **¿Qué hace?** Es una operación terminal que recopila los elementos del Stream y los guarda en una Lista.


```Java
List<Double> precios = List.of(15.50, 8.00, 25.00, 4.99);

// Queremos guardar en una lista nueva solo los precios mayores a 10
List<Double> preciosAltos = precios.stream()
    .filter(precio -> precio > 10.00) // Intermedia: deja pasar 15.50 y 25.00
    .toList(); // Terminal: empaqueta en una lista inmutable (Java 16+)

// Nota: Si usas una versión antigua de Java, verás esto:
// .collect(Collectors.toList());
```

## 3. El Salvador de Errores: `.orElse()` y los Optionals

**¿Cuándo usarlo?** Cuando buscas un elemento específico en la lista, pero existe el riesgo de que la búsqueda no encuentre nada (la lista esté vacía o los filtros descarten todo). **¿Qué hace?** Operaciones terminales como `.findFirst()` o `.max()` devuelven una "caja" llamada `Optional`. El `.orElse()` te permite sacar el valor de la caja o, si está vacía, devolver un valor por defecto, evitando así un `NullPointerException`.


```Java
List<Cliente> clientes = List.of(
    new Cliente("Carlos", "San José"),
    new Cliente("Ana", "Heredia")
);

// Queremos buscar al primer cliente que sea de Limón
String nombreCliente = clientes.stream()
    .filter(c -> c.getCiudad().equals("Limón"))
    .map(Cliente::getNombre)
    .findFirst() // Devuelve un Optional<String>. En este caso, estará vacío.
    .orElse("Cliente no encontrado, revisar base de datos"); // Valor de rescate

System.out.println(nombreCliente); // Imprime: Cliente no encontrado, revisar base de datos
```

## Más Ejemplos Prácticos de Uso Frecuente

### A. Totalizar valores: `.reduce(BinaryOperator)`

**¿Cuándo usarlo?** Para combinar todos los elementos en un solo resultado (como sumar todos los precios de una cotización).


```Java
List<Double> subTotalesCotizacion = List.of(150.0, 50.0, 25.0);

// Empezamos en 0.0, y en cada paso sumamos el acumulador con el precio actual
Double totalPagar = subTotalesCotizacion.stream()
    .reduce(0.0, (acumulador, precio) -> acumulador + precio);

System.out.println("Total de la cotización: $" + totalPagar); // 225.0
```

### B. Validaciones rápidas: `anyMatch` y `allMatch`

**¿Cuándo usarlo?** Cuando solo necesitas un `boolean` para una regla de negocio. Son muy rápidos porque detienen el Stream apenas encuentran la respuesta.


```Java
List<Pedido> pedidos = obtenerPedidosTelegram();

// ¿Hay AL MENOS UN pedido con estado "Pendiente de Pago"?
boolean requiereAtencion = pedidos.stream()
    .anyMatch(pedido -> pedido.getEstado().equals("Pendiente de Pago"));

// ¿TODOS los pedidos ya fueron enviados?
boolean todoListo = pedidos.stream()
    .allMatch(pedido -> pedido.getEstado().equals("Enviado"));
```

### C. Ordenamiento ágil: `.sorted(Comparator)`

**¿Cuándo usarlo?** Para ordenar listas de objetos complejos basándote en alguna de sus propiedades.


```java
List<Producto> inventario = obtenerInventario();

// Ordenamos de menor a mayor precio y devolvemos la lista
List<Producto> catalogoOrdenado = inventario.stream()
    .sorted((p1, p2) -> Double.compare(p1.getPrecio(), p2.getPrecio()))
    .toList();
```

- [[Retos_Streams | Ejercicios para practicar]] 
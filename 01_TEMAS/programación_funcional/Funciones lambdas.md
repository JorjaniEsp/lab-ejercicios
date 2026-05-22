---
Tipo: PF
Tema: Funciones lambdas
---
# Expresiones Lambda e Interfaces Funcionales

## ¿Qué es una Interfaz Funcional?

Para entender las lambdas, primero hay que entender la regla que las hace posibles. Una **Interfaz Funcional** es una interfaz en Java que contiene **un único método abstracto** (sin implementar). 

Se les conoce también como interfaces SAM (*Single Abstract Method*). Son contratos que exigen un solo comportamiento.

> [!INFO] La anotación `@FunctionalInterface`
> ```
Es una buena práctica colocar esta anotación arriba de tu interfaz. No es obligatoria, pero le dice al compilador de Java que vigile que nadie agregue un segundo método abstracto por accidente, lo cual rompería tus lambdas.

### Ejemplo de Interfaz Funcional:

```java
@FunctionalInterface
public interface OperacionMatematica {
    // Solo un método abstracto: el contrato estricto
    int calcular(int a, int b);
}
````

## ¿Qué son las Expresiones Lambda?

Una **expresión lambda** es una función anónima (sin nombre) que sirve para implementar **directamente** el único método de una interfaz funcional.

Si la clase anónima ([[Clases Anónimas|Ver nota]]) era una forma rápida de crear un objeto "desechable", la lambda es la evolución: elimina toda la estructura de la clase y te permite enfocarte **solo en la lógica** (los parámetros y el resultado).

### Sintaxis Básica

La estructura general es: `(parámetros) -> { cuerpo de la función }`

- **`()`**: Los parámetros que recibe el método. Si es un solo parámetro, puedes omitir los paréntesis.
    
- **`->`**: El operador flecha ("lambda"). Separa los parámetros de la lógica.
    
- **`{}`**: El código a ejecutar. Si es una sola línea, puedes omitir las llaves y la palabra `return`.
    

## Evolución: De Clase Anónima a Lambda

Vamos a implementar la interfaz `OperacionMatematica` que creamos arriba para ver cómo el código se vuelve más limpio. Queremos hacer una suma.

### 1. El pasado (Clase Anónima)

Mucho código estructural (_boilerplate_) solo para hacer una suma. 

```java
OperacionMatematica sumaAnonima = new OperacionMatematica() {
    @Override
    public int calcular(int a, int b) {
        return a + b;
    }
};

System.out.println(sumaAnonima.calcular(5, 3)); // Resultado: 8
```

>[!note] nota
>Note que usando clases anónimas nos ahorramos tener que crear una clase formal, osea, un archivo .java para que solo implemente este método y tener que instanciar esa clase y usar el método, pero aún así sigue habiendo mucho ruido en el código.

### 2. El presente (Expresión Lambda)

Java sabe que `OperacionMatematica` solo tiene el método `calcular(int, int)`. Por lo tanto, no necesitas escribir el nombre del método ni los tipos de datos, Java los infiere.

```java
// (a, b) son los parámetros -> a + b es el retorno implícito
OperacionMatematica sumaLambda = (a, b) -> a + b;

System.out.println(sumaLambda.calcular(5, 3)); // Resultado: 8
```

## Ejemplos de uso con diferentes parámetros

Las lambdas se adaptan a lo que exija la interfaz funcional:

**1. Sin parámetros:**

```java
@FunctionalInterface
interface Saludo { void saludar(); }

// Uso:
Saludo miSaludo = () -> System.out.println("¡Hola Mundo!");
miSaludo.saludar();
```

**2. Con un parámetro (se pueden omitir los paréntesis):**

```java
@FunctionalInterface
interface Cuadrado { int calcular(int x); }

// Uso:
Cuadrado miCuadrado = x -> x * x;
System.out.println(miCuadrado.calcular(4)); // Resultado: 16
```

**3. Con múltiples líneas de código (requiere llaves y return):**

```java
OperacionMatematica division = (a, b) -> {
    if (b == 0) {
        System.out.println("Error: División por cero");
        return 0;
    }
    return a / b;
};
```

> [!NOTE]  nota
> El verdadero poder En el día a día, casi no crearás tus propias interfaces funcionales. El poder de las lambdas brilla al inyectar comportamiento directamente en métodos que ya existen en Java, como pasarle una lambda a un botón (`ActionListener`) o a un filtro de una lista.

- [[Interfaces funcionales propias de java | Ver las interfaces propias de java]]
- [[Referencia a métodos| Siguiente tema]]
---
Tipo: PF
Tema: Clases anónimas
---
## ¿Qué son?
Una **clase anónima** es una clase local que no tiene un nombre asignado. Permite declarar e instanciar una clase al mismo tiempo, implementando una interfaz o extendiendo otra clase directamente en el lugar donde se necesita.

## ¿Qué soluciona?
* **Evita el boilerplate (Código repetido):** Evita tener que crear un archivo `.java` separado para una clase que solo vas a usar una única vez en todo el proyecto.
* **Encapsulamiento inmediato:** Permite adjuntar comportamiento directamente al objeto que lo requiere, mejorando la cohesión del código en un entorno puramente orientado a objetos.

---

## ¿Cómo sería SIN la clase anónima?
Para entender el problema, imagina que tenemos una interfaz llamada `Mensajero` y queremos usarla.

### 1. Definición de la Interfaz
```java
public interface Mensajero {
    void emitirMensaje(String nombre, int edad);
}
````

### 2. El enfoque tradicional (Crear una clase física)

Sin clases anónimas, nos vemos obligados a crear una clase formal que implemente la interfaz:

Java

```java
// Archivo: MensajeroEstandar.java
public class MensajeroEstandar implements Mensajero {
    @Override
    public void emitirMensaje(String nombre, int edad) {
        System.out.println("Hola " + nombre + ", tu edad es " + edad);
    }
}
```

### 3. Instanciación en el Main

Java

```java
public class Main {
    public static void main(String[] args) {
        // Tenemos que instanciar la clase formal que creamos antes
        Mensajero mensajero = new MensajeroEstandar();
        mensajero.emitirMensaje("Angely", 21);
    }
}
```

> [!WARNING] Importante
> Desventaja Si necesitas 5 comportamientos distintos en diferentes partes del sistema, tendrías que crear 5 archivos de clase diferentes (`MensajeroEstandar`, `MensajeroFormal`, `MensajeroUrgente`, etc.), llenando el proyecto de clases "desechables".

## Ejemplos con Clase Anónima

Al usar clases anónimas, eliminamos la necesidad de crear el archivo `MensajeroEstandar.java`. Implementamos la lógica "al vuelo".

### Ejemplo 1: Guardada en una variable

Útil si necesitas llamar al método de esa instancia un par de veces dentro del mismo bloque de código.

Java

```java
public class Main {
    public static void main(String[] args) {
        
        // Declaración, implementación e instanciación en un solo paso
        Mensajero lambdaMsje = new Mensajero() {
            @Override
            public void emitirMensaje(String nombre, int edad) {
                System.out.println("Hola desde clase anónima " + nombre);
            }
        };

        // Uso de la instancia
        lambdaMsje.emitirMensaje("TodoCode Suscribite", 25);
    }
}
```

### Ejemplo 2: Pasada directamente como argumento (_Inline_)

Es el caso de uso más común en interfaces gráficas o manejadores de eventos (como el `ActionListener` de Swing). No se almacena en ninguna variable, se pasa directamente al método que la requiere.

Java

```java
import javax.swing.JButton;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

public class EjemploVentana {
    public static void main(String[] args) {
        JButton boton = new JButton("Click aquí");

        // Pasamos la implementación directamente dentro de los paréntesis
        boton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("¡El botón ha sido clickeado!");
            }
        });
    }
}
```

> [!NOTE]  Nota
> ``` 
> Comportamiento del Scope y `this` Dentro de una clase anónima, la palabra clave `this` hace referencia a la propia clase anónima y no a la clase externa que la contiene. Además, solo puede acceder a variables locales del método contenedor si estas son efectivamente finales (`final` o efectivamente inmutables).

- [[Funciones lambdas|Siguiente tema]]


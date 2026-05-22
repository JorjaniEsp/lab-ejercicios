---
Dificultad: Fácil
Tipo: Streams
---
# 🔠 La transformación de mayúsculas

## 🚀 Enunciado:
Crea un método llamado `transformarAMayusculas` que reciba una lista de palabras (`List<String>`). El método debe devolver una **nueva lista** en la que todos los elementos originales hayan sido convertidos íntegramente a letras MAYÚSCULAS.

### 📋 Example:

```java
transformarAMayusculas(List.of("java", "spring", "backend")) 
// ["JAVA", "SPRING", "BACKEND"]
transformarAMayusculas(List.of("Angely", "Limón")) 
// ["ANGELY", "LIMÓN"]
transformarAMayusculas(List.of("UCR")) 
// ["UCR"]
transformarAMayusculas(List.of()) 
// []
````

> [!NOTE] Nota
> 
> - El tamaño de la lista devuelta debe ser exactamente igual al de la original, solo cambia su contenido.
>     
> - Intenta resolver la transformación utilizando una **referencia a método** (`::`) en lugar de una lambda tradicional para que el código quede lo más limpio posible.
>
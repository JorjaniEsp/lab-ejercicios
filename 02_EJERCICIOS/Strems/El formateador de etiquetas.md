---
Dificultad: Medio
Tipo: Streams
---
# 🏷️ El formateador de etiquetas

## 🚀 Enunciado:
Crea un método llamado `formatearEtiquetas` que reciba una lista de palabras clave (`List<String>`). El método debe devolver un **único texto** (`String`) donde cada palabra de la lista original haya sido convertida a minúsculas, tenga el símbolo `#` concatenado al inicio, y todas las palabras resultantes estén unidas por una coma y un espacio (`, `).

### 📋 Example:

```java
formatearEtiquetas(List.of("Java", "Spring", "API"))
 // "#java, #spring, #api"
formatearEtiquetas(List.of("Backend")) 
// "#backend"
formatearEtiquetas(List.of("BasesDeDatos", "SQL")) 
// "#basesdedatos, #sql"
formatearEtiquetas(List.of()) 
// ""
````

> [!NOTE] Nota
> 
> - Para lograr este resultado, necesitarás encadenar operaciones. Primero, una operación intermedia (`.map()`) que se encargue de manipular individualmente cada texto (minúsculas + hashtag).
>     
> - Segundo, para convertir ese flujo de textos sueltos en un solo gran `String`, busca información sobre la clase utilitaria `Collectors` y su potente método terminal `.joining()`.
>
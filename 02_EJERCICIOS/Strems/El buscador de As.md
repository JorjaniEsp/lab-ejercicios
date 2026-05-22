---
Dificultad: Fácil
Tipo: Streams
---
# 🧩 El buscador de As

## 🚀 Enunciado:
Crea un método llamado `buscarNombresConA` que reciba una lista de cadenas (`List<String>`). El método debe devolver una **nueva lista** que contenga únicamente los nombres que comiencen con la letra 'A', sin importar si el usuario los escribió en mayúscula o minúscula.

### 📋 Example:

```java
buscarNombresConA(List.of("Angely", "Jorjanie", "ana", "Pedro")) // ["Angely", "ana"]
buscarNombresConA(List.of("Carlos", "Luis")) // []
buscarNombresConA(List.of("Alba", "Alberto", "Amanda")) // ["Alba", "Alberto", "Amanda"]
buscarNombresConA(List.of()) // []
````

> [!NOTE] Nota
> 
> - El filtro debe ser insensible a mayúsculas y minúsculas (tanto 'A' como 'a' son válidas).
>     
> - Si la lista original está vacía o ningún nombre cumple la condición, debe retornar una lista vacía, nunca `null`.
>
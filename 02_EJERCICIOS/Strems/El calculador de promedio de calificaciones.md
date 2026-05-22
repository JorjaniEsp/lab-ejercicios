---
Dificultad: Medio
Tipo: Streams
---
# 📊 El calculador de promedio de calificaciones

## 🚀 Enunciado:
Crea un método llamado `calcularPromedio` que reciba una lista de calificaciones enteras (`List<Integer>`). El método debe calcular y devolver el promedio exacto incluyendo sus decimales (`double`). 

### 📋 Example:

```java
calcularPromedio(List.of(80, 90, 100)) 
// 90.0
calcularPromedio(List.of(70, 85, 77)) 
// 77.33333333333333
calcularPromedio(List.of(65)) 
// 65.0
calcularPromedio(List.of()) 
// 0.0
````

> [!NOTE] Nota
> 
> - Recuerda que un `Stream<Integer>` maneja _objetos_. Para habilitar operaciones matemáticas directas (como la suma o el promedio), es muy útil transformar ese flujo de objetos a un flujo de datos primitivos usando la operación intermedia `.mapToInt()`.
>     
> - La operación terminal para promediar es `.average()`. Como existe el riesgo de que la lista original esté vacía (y no se puede dividir entre cero), esta operación devuelve un `OptionalDouble`. ¡Asegúrate de encadenar un `.orElse()` para devolver `0.0` en caso de que la caja esté vacía!
>
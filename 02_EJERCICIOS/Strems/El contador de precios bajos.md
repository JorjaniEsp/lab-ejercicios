---
Dificultad: Fácil 
Tipo: Streams 
---
# 📉 El contador de precios bajos 
## 🚀 Enunciado: 
Crea un método llamado `contarPreciosBajos` que reciba una lista de precios (`List<Double>`) y un precio límite (`double`). El método debe devolver la **cantidad total** de precios que sean estrictamente menores a ese límite establecido. 
### 📋 Example: 

```java 
contarPreciosBajos(List.of(15.5, 9.99, 25.0, 4.50), 10.0) 
// 2 
contarPreciosBajos(List.of(50.0, 100.0, 15.0), 20.0) 
// 1 
contarPreciosBajos(List.of(5.0, 8.5), 10.0) 
// 2 
contarPreciosBajos(List.of(10.0, 20.0), 10.0) 
// 0
```

>[!NOTE] Nota
>- Recuerda que la operación terminal que cuenta elementos en un Stream (`.count()`) no devuelve un `int`, sino un `long`. Asegúrate de que la firma de tu método devuelva el tipo de dato correcto.
>
>- "Estrictamente menores" significa que si el precio es igual al límite, no debe contarse.





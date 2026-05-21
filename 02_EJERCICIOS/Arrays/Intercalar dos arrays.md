---
Dificultad: Fácil
Tipo: Arrays
---
## 🧩Enunciado:
Dados dos arrays de cualquier tipo, devuelve un nuevo array con los elementos intercalados: primero el elemento 0 del array A, luego el elemento 0 del array B, después el elemento 1 del array A, el elemento 1 del array B, y así sucesivamente. Si un array es más largo que el otro, los elementos sobrantes se agregan al final del resultado. 

>[!Example]
>```java
>Ejemplos intercalateArrays(new int[]{1, 2, 3}, new String[]{"a", "b", "c"})
>// Resultado: [1, "a", 2, "b", 3, "c"] 
>intercalateArrays(new int[]{1, 2}, new String[]{"a", "b", "c", "d"}) 
>// Resultado: [1, "a", 2, "b", "c", "d"] 
>intercalateArrays(new int[]{}, new int[]{10, 20}) 
>// Resultado: [10, 20] 

>[!Note] Notas
>```
> - Los parámetros arrayA y arrayB son de tipo Object porque pueden recibir int[], boolean[], String[], etc. 
> - No modifiques los arrays originales. 
> - El orden de intercalación es siempre: elemento del primer array, elemento del segundo array.


---
-->[[Solucion_Intercalar_Array | Mi solucón]]

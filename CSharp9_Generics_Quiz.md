
# 🧠 C# 9 Generics — Quiz de Preparación

Este cuestionario está diseñado para ayudarte a repasar los conceptos clave del curso *C# 9 Generics* de Pluralsight. Contiene preguntas de opción múltiple basadas en los módulos del curso.

---

## ❓ Preguntas

### 1. ¿Cuál de las siguientes opciones **no** es una ventaja de usar genéricos en C#?
a) Reutilización de código  
b) Seguridad de tipos en tiempo de compilación  
c) Mejora de rendimiento al evitar boxing  
d) Acceso directo a miembros privados de una clase  

**Respuesta:** d  
**Explicación:** Los genéricos no otorgan acceso especial a miembros privados.

---

### 2. ¿Cuál es el problema principal al usar `object` en vez de generics?
a) Requiere más memoria  
b) No se puede compilar  
c) Pierde seguridad de tipo y puede generar casting inválido  
d) Es más difícil de leer  

**Respuesta:** c  
**Explicación:** Usar `object` elimina la seguridad de tipos, lo que puede provocar errores en tiempo de ejecución.

---

### 3. ¿Qué significa el modificador `out` en una interfaz genérica como `IReadRepository<out T>`?
a) Solo permite tipos primitivos  
b) El tipo se puede usar solo como retorno (covarianza)  
c) El tipo es contravariante  
d) Se puede usar en structs únicamente  

**Respuesta:** b  
**Explicación:** `out` indica covarianza: el tipo solo puede usarse como retorno.

---

### 4. ¿Qué ocurre si se declara una variable estática dentro de una clase genérica `Container<T>`?
a) Es compartida por todas las instancias de todos los tipos  
b) Se crea una copia única por tipo `T`  
c) No se puede compilar  
d) Es la misma para tipos de referencia y de valor  

**Respuesta:** b  
**Explicación:** Cada tipo genérico `T` tiene su propia copia de los miembros estáticos.

---

### 5. ¿Cuál de estas clases representa un patrón común de restricción genérica?
a) `where T : static`  
b) `where T : IEntity`  
c) `where T : sealed`  
d) `where T : string`  

**Respuesta:** b  
**Explicación:** Las restricciones genéricas comunes incluyen herencia o interfaces (`IEntity`, `class`, `new()`).

---

### 6. ¿Qué tipo de delegado debe usarse para seguir el patrón de eventos estándar en .NET?
a) `Action<T>`  
b) `Func<T>`  
c) `EventHandler<T>`  
d) `Predicate<T>`  

**Respuesta:** c  
**Explicación:** `EventHandler<T>` es el delegado estándar para eventos en .NET.

---

### 7. ¿Qué se requiere para poder usar el operador `+` en un método genérico con `T`?
a) Usar `dynamic` para los operandos  
b) Usar `where T : operator+`  
c) Crear una clase base para tipos numéricos  
d) Solo es posible con tipos de referencia  

**Respuesta:** a  
**Explicación:** No se puede aplicar `+` directamente sobre `T`, pero sí usando `dynamic`.

---

### 8. ¿Qué hace el siguiente código?

```csharp
public void PrintItem<TItem>(TItem item)
{
    Console.WriteLine(item);
}
```

a) Lanza excepción si `item` es null  
b) Es un método genérico dentro de una clase genérica  
c) Solo acepta `string`  
d) Requiere un tipo `TItem` que implemente `IEntity`  

**Respuesta:** b  
**Explicación:** Es un método genérico independiente del tipo de la clase que lo contiene.

---

### 9. ¿Qué permite la contravarianza (`in T`) en un delegado o interfaz?
a) Usar tipos más genéricos como argumento  
b) Usar el tipo solo como retorno  
c) Usar tipos más específicos como argumento  
d) Convertir interfaces genéricas a strings  

**Respuesta:** c  
**Explicación:** Contravarianza permite pasar un `IWriteRepository<Manager>` a un método que espera `IWriteRepository<Employee>`.

---

### 10. ¿Qué beneficio adicional tiene usar métodos de extensión genéricos?
a) Solo sirven para LINQ  
b) Pueden aplicarse sobre cualquier tipo específico sin modificar la clase original  
c) No pueden tener restricciones de tipo  
d) No se pueden usar con interfaces  

**Respuesta:** b  
**Explicación:** Los métodos de extensión permiten extender tipos sin herencia ni modificar código original.

---

¡Buena suerte en tu examen de Pluralsight! 🚀

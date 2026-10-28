# Evidencias: <José Manuel Botero Giraldo>

## 1. Errores de sintaxis corregidos
| # | Archivo | Línea | Mensaje del compilador | Corrección |
|---|---------|-------|------------------------|------------|
| 1 | Identificable.java | 4 | `';' expected` | Añadí ; |
| 2 | Acompanamiento.java | 14 | `';' expected` | Añadí ; |
| 3 | Ingrediente.java | 67 | `unclosed string literal` | Añadi " |
| 4 | Verdura.java | 3 | `'{' expected` | Añadí "s" a extends |
| 5 | Tuberculo.java | 6 | `invalid method declaration; return type required` | Elimine "s" exdente.|
| 6 | Tuberculo.java | 22 | `unclosed character literal` | Remplace ` por " |
| 7 | Fonda.java | 8 | `cannot find symbol: class ArrayList` | import java.util.ArrayList; con la ayuda dinamica |
| 8 | Olla.java | 64 | `cannot find symbol: variable length` | Se remplaza length a size |
| 9 | Ingrediente.java | 25 | `incompatible types: possible lossy conversion from double to int` | public int a double |
| 10 | Ingrediente.java | 37 | `cannot find symbol: method IllegalArgumentException(String)` | se agrega "new"|
| 11 | Costeable.java | 5 | `interface abstract methods cannot have body` | Quité el cuerpo: "double calcularCosto();" |
| 12 | Acompanamiento.java | 4/16 | `is not abstract and does not override abstract method calcularCosto() in Costeable` | Renombré `"calcularPrecio()" a "calcularCosto()" |
| 13 | Sancocho.java | 34 | `non-static method calcularTiempoCoccion() cannot be referenced from a static context` | Se corrije mayuscula |
| 14 | Sancocho.java | 55–60 (y Fonda.java 47) | `incompatible types: unexpected return value` / `'void' type not allowed here` | "servir" se cambia a bolean |
| 15 | Proteina.java | 8 | `constructor Ingrediente ... cannot be applied to given types` | Se agrego "fresco" a lista |
| 16 | Proteina.java | 18 | `incompatible types: String cannot be converted to int` | Se quitan "" es int |
| 17 | Pedido.java | 33 | `cannot find symbol: variable getPrecio` | Se agregan () |
| 18 | Verdura.java | 3 y 10 | `is not abstract and does not override abstract method minutosCoccion()` / `method does not override or implement a method from a supertype` | El método se llamaba "minutosDeCoccion" lo renombré a "minutosCoccion" |
| 19 | Condimento.java | 9 | `cannot find symbol: variable alFinal` | Se corrije parametro "seAgregaAlFinal" |
| 20 | Main.java | 23 | `Ingrediente is abstract; cannot be instantiated` | "new Ingrediente(...)" a "new Tuberculo(...)" |
| 21 | Main.java | 108 | `incompatible types: Ingrediente cannot be converted to Proteina` | Se agrega "Proteina" |
| 22 | Fonda.java | 47 | `constructor Pedido ... cannot be applied to given types` | se agrega "cantidad" |
| 23 | Fonda.java | 65 | `package system does not exist` | "system.out" → "System.out" |
| 24 | Condimento.java | 18–23 | `variable minutos might not have been initialized` | Cambié "else if (!seAgregaAlFinal)" por "else" |
| 25 | Olla.java | 45–51 | `missing return statement` | Agregué "return null;" al final de "buscarPorCodigo" |

## 2. Errores de lógica corregidos
| # | Archivo y método | Qué hacía mal | Pista (fila de la tabla) | Cómo lo corregí |
|---|------------------|---------------|--------------------------|-----------------|
| 1 | Ingrediente.calcularCosto | gramos - 1000 es división entera: 600 g daban 0 y casi todos los ingredientes costaban $0 | Fichas con $0; la gallina de 1500 g costaba $18000 en vez de $27000 | gramos - 1000.0 * precioKilo |
| 2 | Olla.agregarIngrediente | Revisaba el peso actual y no sumaba el del ingrediente nuevo, así que la olla se pasaba de la capacidad | Olla pequeña 1130/1000 g y «¿Cupo la yuca? true» | calcularPesoTotal() + nuevo.getGramos() > capacidadGramos |
| 3 | Olla.buscarPorCodigo | Comparaba el **nombre** con el código, por eso nunca encontraba nada (tampoco detectaba códigos repetidos) | «¿Se aceptó un código repetido? true» y «Buscar PRO-001: no encontrado» | i.getCodigo().equals(codigo) |
| 4 | Olla.calcularCostoIngredientes | El for empezaba en i = 1 y se saltaba el primer ingrediente | Costo del sancocho menor al real | Empezar en i = 0 |
| 5 | Olla.calcularTiempoCoccion | Usaba <, devolvía el menor (siempre 0) en vez del mayor | Fichas de sancocho con 0 min | Cambié a i.minutosCoccion() > mayor |
| 6 | Tuberculo.minutosCoccion | Valores invertidos: el duro daba 25 y el blando 40 | Papa (blanda) con 40 min y yuca (dura) con 25 min | return duro ? 40 : 25; |
| 7 | Sancocho.estaCompleto | Mezclaba && con ||, bastaba tener condimento para estar «completo» | «¿El caldo de papa está completo? true» (no tiene proteína) | Exigir las tres condiciones con && |
| 8 | Sancocho.esTrifasico | Contaba todos los ingredientes, no las proteínas | «¿El de gallina es trifásico? true» (solo tiene 1 proteína) | olla.contarPorCategoria("Proteína") >= 3 |
| 9 | Pedido.calcularCosto | Los acompañamientos se sumaban una sola vez en lugar de multiplicarse por la cantidad | Mesa 1: $5700 no cuadraba con «cada plato lleva sus acompañamientos» | (precioPorción + sumaAcompanamientos) * cantidad |
| 10 | Fonda.registrarPedido | Guardaba el pedido en la lista antes de verificar las porciones; los pedidos fallidos quedaban registrados y sumaban a las ventas | «Pedidos registrados: 4» cuando solo 3 fueron válidos | Llamar a servir(cantidad) primero y crear/agregar el Pedido solo si alcanzan |

## 3. Salida final del programa
(pega aquí la salida completa de `java -cp out Main`, o una captura)

## 4. Conceptos de POO en este proyecto
Explica brevemente (2-3 líneas cada uno) DÓNDE se usa en este código:
- **Encapsulamiento:**
- **Herencia:**
- **Abstracción (clase abstracta):**
- **Interfaz:** (hay dos, ¿qué clases implementa cada una?)
- **Polimorfismo:** (mira la sección 6 de Main)
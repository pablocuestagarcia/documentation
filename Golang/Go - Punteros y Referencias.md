En Go, no existen los conceptos tradicionales de punteros y referencias como se encuentran en otros lenguajes de programación. Sin embargo, Go utiliza un enfoque basado en valores y referencias para lograr resultados similares. 

En Go, todas las variables son pasadas por valor de forma predeterminada, lo que significa que se crea una copia de la variable cada vez que se pasa como argumento a una función o se asigna a otra variable. Esto es diferente de los lenguajes que utilizan punteros o referencias explícitas para modificar valores en su ubicación original.

Sin embargo, Go proporciona una manera de simular el comportamiento de los punteros utilizando el operador "&" (ampersand) para obtener la dirección de memoria de una variable y el operador "\*" (asterisco) para desreferenciar un puntero y acceder al valor al que apunta.

Aquí hay un ejemplo para ilustrar esto:

```go
func main() {
    x := 10

    // Puntero
    y := &x

    fmt.Println("Valor de x:", x)     // Imprime "Valor de x: 10"
    fmt.Println("Dirección de x:", y) // Imprime "Dirección de x: 0xc000014078"
    fmt.Println("Valor de y:", *y)    // Imprime "Valor de y: 10"

    // Modificar el valor a través del puntero
    *y = 20
    fmt.Println("Nuevo valor de x:", x) // Imprime "Nuevo valor de x: 20"
}
```

En este ejemplo, `x` es una variable que contiene el valor 10. Luego, creamos un puntero `y` que apunta a la dirección de memoria de `x` utilizando el operador "&". Al imprimir `y`, obtenemos la dirección de memoria de `x`. Al desreferenciar `y` usando el operador "\*", podemos acceder al valor al que apunta, que es 10.

Al modificar el valor a través del puntero utilizando el operador "\*", también se modifica el valor original de `x`. Por lo tanto, cuando imprimimos `x` nuevamente, obtendremos el nuevo valor, que es 20.

En cuanto al uso de punteros en Go, generalmente se utilizan en los siguientes casos:

1. Pasar valores grandes a funciones sin tener que copiarlos en su totalidad.
2. Modificar valores en su ubicación original, especialmente cuando se trata de estructuras de datos complejas.
3. Permitir que las funciones modifiquen valores pasados como argumentos.

En resumen, aunque Go no tiene punteros y referencias explícitas como en otros lenguajes, puedes lograr un comportamiento similar utilizando el operador "&" para obtener la dirección de memoria de una variable y el operador "\*" para desreferenciar un puntero y acceder al valor al que apunta.

* `&` obtiene la dirección de memoria de una variable
* `*` desreferencia un punterio y accede al valor al que apunta.


## Propiedad en Go

En Go, cuando pasas una estructura de datos como argumento a una función o la asignas a otra variable, se realiza una copia de la estructura de datos por valor. Esto significa que se crea una nueva instancia de la estructura de datos y se copian todos los valores de los campos en la nueva instancia.

Aquí hay un ejemplo para ilustrar esto:

```go
type Person struct {
    Name string
    Age  int
}

func main() {
    p1 := Person{Name: "Alice", Age: 25}

    // Pasar la estructura de datos a una función
    modifyPerson(p1)
    fmt.Println("Valor de p1 después de llamar a la función:", p1) // Imprime "Valor de p1 después de llamar a la función: {Alice 25}"

    // Asignar la estructura de datos a otra variable
    p2 := p1
    p2.Name = "Bob"
    fmt.Println("Valor de p1 después de asignar a p2:", p1) // Imprime "Valor de p1 después de asignar a p2: {Alice 25}"
    fmt.Println("Valor de p2:", p2)                       // Imprime "Valor de p2: {Bob 25}"
}

func modifyPerson(p Person) {
    p.Name = "Eve"
    p.Age = 30
}
```

En este ejemplo, tenemos una estructura de datos llamada `Person` con dos campos: `Name` y `Age`. Creamos una instancia `p1` de `Person` con valores "Alice" y 25. Luego, pasamos `p1` a la función `modifyPerson`.

Dentro de la función `modifyPerson`, se modifica el valor del campo `Name` a "Eve" y el valor del campo `Age` a 30. Sin embargo, esto solo afecta a la copia local de la estructura `p` dentro de la función y no modifica el valor original de `p1` fuera de la función.

Después de llamar a la función `modifyPerson` y asignar `p1` a `p2`, podemos ver que el valor de `p1` no ha cambiado. Esto se debe a que se realizó una copia por valor cuando pasamos `p1` a la función y cuando asignamos `p1` a `p2`. Cualquier modificación realizada en `p` dentro de la función o en `p2` no afecta al valor original de `p1`.

Es importante tener en cuenta que las estructuras de datos más grandes pueden generar una sobrecarga en la copia por valor. En esos casos, es posible utilizar punteros para pasar la referencia de la estructura y evitar copiarla completamente.
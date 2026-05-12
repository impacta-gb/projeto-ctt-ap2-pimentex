# 03 - Estruturas de Controle

No Go, o fluxo de controle é direto. Uma característica única: **não existe o laço `while`**, o `for` é utilizado para todas as repetições.

!!! info "Sintaxe sem parênteses"
    Em Go, você não utiliza parênteses `()` em condições de `if` ou `for`.

```go
package main
import "fmt"

func main() {
    estoque := 10

    // If/Else
    if estoque > 0 {
        fmt.Println("Produto em estoque")
    } else {
        fmt.Println("Esgotado")
    }

    // For (como While)
    i := 0
    for i < 3 {
        fmt.Println("Tentativa:", i)
        i++
    }
}
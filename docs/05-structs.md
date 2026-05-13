# 05 - Structs e Métodos

Go não possui classes, mas utiliza `structs` para agrupar campos de dados e métodos para definir comportamentos.

```go
package main
import "fmt"

type Pedido struct {
    ID    int
    Total float64
}

// Método associado à struct Pedido
func (p Pedido) Exibir() {
    fmt.Printf("Pedido #%d - Total: R$%.2f\n", p.ID, p.Total)
}

func main() {
    meuPedido := Pedido{ID: 123, Total: 250.50}
    meuPedido.Exibir()
}
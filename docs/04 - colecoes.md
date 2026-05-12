# 04 - Arrays, Slices e Maps

Go oferece formas eficientes de agrupar dados.

* **Arrays:** Tamanho fixo.
* **Slices:** Dinâmicos (mais comuns).
* **Maps:** Coleções de chave-valor.

!!! tip "Use Slices"
    Slices são mais flexíveis que Arrays e permitem o uso da função `append()`.

```go
package main
import "fmt"

func main() {
    // Slice
    produtos := []string{"Teclado", "Mouse"}
    produtos = append(produtos, "Monitor")

    // Map
    precos := map[string]float64{
        "Teclado": 150.00,
        "Mouse": 50.00,
    }
    fmt.Println(produtos, precos)
}
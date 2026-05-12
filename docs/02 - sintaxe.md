# Sintaxe Básica e Variáveis

A linguagem Go possui uma sintaxe limpa e minimalista. Uma das suas maiores características é ser estaticamente tipada, mas possuir um mecanismo inteligente de inferência de tipos.

!!! warning "Cuidado com variáveis não utilizadas"
    No Go, declarar uma variável e não utilizá-la no código resultará em um **erro de compilação**. O Go foi desenhado para manter o código limpo e livre de desperdícios!

## Declarando Variáveis na Prática

Você pode declarar variáveis de forma explícita usando a palavra reservada `var`, ou usar o operador de declaração curta `:=` (que infere o tipo automaticamente e é o mais usado no dia a dia).

Veja o exemplo abaixo simulando o cadastro de um produto em uma loja:

```go
package main

import "fmt"

func main() {
    // Declaração explícita (Longa)
    var nomeProduto string = "Teclado Mecânico"
    var quantidade int = 50
    
    // Declaração curta (Inferência de tipo) - Mais recomendada!
    preco := 299.90
    emEstoque := true

    fmt.Println("Produto:", nomeProduto)
    fmt.Println("Quantidade:", quantidade)
    fmt.Println("Preço: R$", preco)
    fmt.Println("Disponível:", emEstoque)
}
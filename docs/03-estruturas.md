# Estruturas de Controle

As estruturas de controle são responsáveis por definir o fluxo de execução de um programa. Em Go, as principais estruturas utilizadas são:

- `if`
- `for`
- `switch`

Essas estruturas permitem criar decisões, repetições e fluxos condicionais de forma simples e eficiente.

---

## Estrutura `if`

A estrutura `if` é utilizada para executar blocos de código apenas quando uma condição é verdadeira.

### Sintaxe básica

```go
if condição {
    // código executado se a condição for verdadeira
}
```

---

## Exemplo simples com `if`

```go
package main

import "fmt"

func main() {

    idade := 20

    if idade >= 18 {
        fmt.Println("Maior de idade")
    }
}
```

---

## Estrutura `if` e `else`

O bloco `else` é executado quando a condição do `if` for falsa.

### Exemplo

```go
package main

import "fmt"

func main() {

    idade := 16

    if idade >= 18 {
        fmt.Println("Maior de idade")
    } else {
        fmt.Println("Menor de idade")
    }
}
```

---

## Estrutura `if else if`

Permite testar múltiplas condições.

### Exemplo

```go
package main

import "fmt"

func main() {

    nota := 7

    if nota >= 9 {
        fmt.Println("Excelente")
    } else if nota >= 7 {
        fmt.Println("Aprovado")
    } else {
        fmt.Println("Reprovado")
    }
}
```

---

## Declaração curta dentro do `if`

Go permite criar variáveis diretamente na condição.

### Exemplo

```go
package main

import "fmt"

func main() {

    if idade := 20; idade >= 18 {
        fmt.Println("Maior de idade")
    }
}
```

!!! tip "Dica de Ouro"
    Variáveis declaradas dentro do `if` existem apenas dentro daquele bloco de código.

---

## Operadores relacionais

Os operadores relacionais são muito utilizados em estruturas condicionais.

| Operador | Significado |
|---|---|
| `==` | Igual |
| `!=` | Diferente |
| `>` | Maior |
| `<` | Menor |
| `>=` | Maior ou igual |
| `<=` | Menor ou igual |

---

## Operadores lógicos

| Operador | Significado |
|---|---|
| `&&` | E lógico |
| `||` | OU lógico |
| `!` | NÃO lógico |

### Exemplo

```go
package main

import "fmt"

func main() {

    idade := 25
    possuiCNH := true

    if idade >= 18 && possuiCNH {
        fmt.Println("Pode dirigir")
    }
}
```

---

## Estrutura `for`

Em Go, o `for` é a única estrutura de repetição da linguagem.

Ela pode substituir:

- `while`
- `do while`
- loops tradicionais

---

## `for` tradicional

### Exemplo

```go
package main

import "fmt"

func main() {

    for i := 1; i <= 5; i++ {
        fmt.Println(i)
    }
}
```

---

## Explicando o `for`

| Parte | Função |
|---|---|
| `i := 1` | Inicialização |
| `i <= 5` | Condição |
| `i++` | Incremento |

---

## `for` como `while`

Go não possui `while`. O comportamento é feito utilizando `for`.

### Exemplo

```go
package main

import "fmt"

func main() {

    contador := 1

    for contador <= 5 {

        fmt.Println(contador)

        contador++
    }
}
```

---

## Loop infinito

### Exemplo

```go
package main

import "fmt"

func main() {

    for {
        fmt.Println("Executando...")
    }
}
```

!!! warning "Cuidado"
    Loops infinitos podem consumir muitos recursos do sistema caso não possuam uma condição de parada adequada.

---

## Utilizando `break`

O `break` interrompe completamente o loop.

### Exemplo

```go
package main

import "fmt"

func main() {

    for i := 1; i <= 10; i++ {

        if i == 5 {
            break
        }

        fmt.Println(i)
    }
}
```

---

## Utilizando `continue`

O `continue` ignora a iteração atual e continua o loop.

### Exemplo

```go
package main

import "fmt"

func main() {

    for i := 1; i <= 5; i++ {

        if i == 3 {
            continue
        }

        fmt.Println(i)
    }
}
```

---

## Estrutura `switch`

O `switch` é utilizado para múltiplas condições de forma mais organizada.

---

## Exemplo simples com `switch`

```go
package main

import "fmt"

func main() {

    dia := 3

    switch dia {

    case 1:
        fmt.Println("Domingo")

    case 2:
        fmt.Println("Segunda")

    case 3:
        fmt.Println("Terça")

    default:
        fmt.Println("Dia inválido")
    }
}
```

---

## `switch` sem expressão

Go permite utilizar `switch` sem variável definida.

### Exemplo

```go
package main

import "fmt"

func main() {

    nota := 8

    switch {

    case nota >= 9:
        fmt.Println("Excelente")

    case nota >= 7:
        fmt.Println("Aprovado")

    default:
        fmt.Println("Reprovado")
    }
}
```

---

## Múltiplos valores no `case`

### Exemplo

```go
package main

import "fmt"

func main() {

    letra := "a"

    switch letra {

    case "a", "e", "i", "o", "u":
        fmt.Println("Vogal")

    default:
        fmt.Println("Consoante")
    }
}
```

---

## Diferença entre `if` e `switch`

| Estrutura | Melhor uso |
|---|---|
| `if` | Poucas condições |
| `switch` | Muitas comparações |
| `for` | Repetições e loops |

---

## Boas práticas com estruturas de controle

| Boa prática | Motivo |
|---|---|
| Evitar muitos `if` aninhados | Facilita leitura |
| Utilizar `switch` em múltiplos casos | Código mais organizado |
| Evitar loops infinitos desnecessários | Melhor performance |
| Utilizar nomes claros nas condições | Facilita manutenção |

!!! tip "Dica de Ouro"
    Código limpo e legível é uma das filosofias mais importantes da linguagem Go.

---

## Exemplo completo

```go
package main

import "fmt"

func main() {

    for i := 1; i <= 10; i++ {

        if i%2 == 0 {

            switch {

            case i == 2:
                fmt.Println("Número 2")

            case i == 4:
                fmt.Println("Número 4")

            default:
                fmt.Printf("Número par: %d\n", i)
            }
        }
    }
}
```

---

## Próximos passos

Agora que já entendemos estruturas condicionais e loops, o próximo passo é aprender como trabalhar com coleções de dados em Go.

➡️ [Arrays, Slices e Maps](04-colecoes.md)

---

## Resumo

Nesta página aprendemos:

- Estrutura `if`
- Estrutura `else`
- Estrutura `switch`
- Loops com `for`
- Operadores relacionais
- Operadores lógicos
- Controle de repetição
- Uso de `break` e `continue`

!!! note "Resumo Final"
    Estruturas de controle são fundamentais para criar aplicações dinâmicas, inteligentes e organizadas. Em Go, essas estruturas foram projetadas para serem simples, eficientes e fáceis de manter.
# Sintaxe Básica e Variáveis

Após instalar o Go e configurar o ambiente, o próximo passo é compreender a sintaxe básica da linguagem e como declarar variáveis corretamente.

A sintaxe do Go foi projetada para ser simples, legível e eficiente, reduzindo ambiguidades e facilitando a manutenção do código.

---

## Estrutura básica de um programa Go

Todo programa em Go segue uma estrutura inicial padrão.

### Exemplo básico

```go
package main

import "fmt"

// Função principal do programa
func main() {

    // Exibe uma mensagem no terminal
    fmt.Println("Olá, mundo!")
}
```

---

## Entendendo cada parte do código

| Elemento | Função |
|---|---|
| `package main` | Define o pacote principal |
| `import` | Importa bibliotecas |
| `func main()` | Função principal executada pelo programa |
| `fmt.Println()` | Exibe mensagens no terminal |

!!! note "Nota Importante"
    Todo programa executável em Go precisa obrigatoriamente do pacote `main` e da função `main()`.

---

## Comentários em Go

Comentários são utilizados para documentar e explicar o código.

### Comentário de uma linha

```go
// Isto é um comentário
fmt.Println("Go")
```

### Comentário de múltiplas linhas

```go
/*
Este é um comentário
de múltiplas linhas
*/
fmt.Println("Go")
```

---

## Declaração de variáveis

Variáveis são utilizadas para armazenar valores na memória.

Em Go, existem diferentes formas de declarar variáveis.

---

## Declarando variáveis com `var`

### Exemplo

```go
package main

import "fmt"

func main() {

    var nome string = "Pedro"
    var idade int = 22

    fmt.Println(nome)
    fmt.Println(idade)
}
```

---

## Inferência de tipos

O Go consegue identificar automaticamente o tipo da variável.

### Exemplo

```go
package main

import "fmt"

func main() {

    var cidade = "São Paulo"
    var temperatura = 25

    fmt.Println(cidade)
    fmt.Println(temperatura)
}
```

!!! tip "Dica de Ouro"
    A inferência de tipos reduz código desnecessário e torna a leitura mais limpa.

---

## Declaração curta com `:=`

A forma mais comum de criar variáveis em Go é utilizando `:=`.

### Exemplo

```go
package main

import "fmt"

func main() {

    nome := "Maria"
    idade := 30

    fmt.Println(nome)
    fmt.Println(idade)
}
```

!!! warning "Cuidado"
    O operador `:=` só pode ser utilizado dentro de funções.

---

## Tipos primitivos em Go

Go possui diversos tipos primitivos integrados.

### Principais tipos

| Tipo | Descrição | Exemplo |
|---|---|---|
| `string` | Texto | `"Go"` |
| `int` | Número inteiro | `10` |
| `float64` | Número decimal | `3.14` |
| `bool` | Verdadeiro ou falso | `true` |
| `byte` | Valor binário | `255` |
| `rune` | Caracter Unicode | `'A'` |

---

## Trabalhando com strings

### Exemplo

```go
package main

import "fmt"

func main() {

    mensagem := "Aprendendo Go"

    fmt.Println(mensagem)
}
```

---

## Trabalhando com números inteiros

### Exemplo

```go
package main

import "fmt"

func main() {

    idade := 25
    ano := 2026

    fmt.Println(idade)
    fmt.Println(ano)
}
```

---

## Trabalhando com números decimais

### Exemplo

```go
package main

import "fmt"

func main() {

    preco := 19.99

    fmt.Println(preco)
}
```

---

## Trabalhando com booleanos

### Exemplo

```go
package main

import "fmt"

func main() {

    ativo := true
    admin := false

    fmt.Println(ativo)
    fmt.Println(admin)
}
```

---

## Constantes em Go

Constantes armazenam valores que não podem ser alterados.

### Exemplo

```go
package main

import "fmt"

func main() {

    const pi = 3.14159

    fmt.Println(pi)
}
```

!!! note "Nota Importante"
    Utilize constantes para valores fixos como PI, URLs, portas e configurações permanentes.

---

## Múltiplas variáveis

Go permite declarar várias variáveis ao mesmo tempo.

### Exemplo

```go
package main

import "fmt"

func main() {

    var (
        nome  = "Carlos"
        idade = 28
        ativo = true
    )

    fmt.Println(nome)
    fmt.Println(idade)
    fmt.Println(ativo)
}
```

---

## Zero Values em Go

Quando uma variável é criada sem valor inicial, Go atribui automaticamente um valor padrão.

| Tipo | Valor padrão |
|---|---|
| `int` | `0` |
| `float64` | `0.0` |
| `string` | `""` |
| `bool` | `false` |

### Exemplo

```go
package main

import "fmt"

func main() {

    var nome string
    var idade int
    var ativo bool

    fmt.Println(nome)
    fmt.Println(idade)
    fmt.Println(ativo)
}
```

---

## Formatação de saída com `Printf`

O `Printf` permite formatar a saída de dados.

### Principais formatações

| Formato | Descrição |
|---|---|
| `%s` | String |
| `%d` | Inteiro |
| `%f` | Decimal |
| `%t` | Booleano |

### Exemplo

```go
package main

import "fmt"

func main() {

    nome := "Ana"
    idade := 20

    fmt.Printf("Nome: %s\n", nome)
    fmt.Printf("Idade: %d\n", idade)
}
```

---

## Convenções de nomenclatura

Go utiliza padrões simples e consistentes.

| Convenção | Exemplo |
|---|---|
| camelCase | `nomeCompleto` |
| PascalCase | `NomeCompleto` |
| Nomes curtos e claros | `idade`, `usuario`, `email` |

!!! tip "Dica de Ouro"
    Em Go, nomes iniciados com letra maiúscula tornam-se públicos/exportáveis para outros pacotes.

---

## Boas práticas com variáveis

| Boa prática | Motivo |
|---|---|
| Utilizar nomes claros | Facilita manutenção |
| Evitar nomes genéricos | Reduz ambiguidades |
| Preferir inferência de tipos | Código mais limpo |
| Utilizar constantes quando possível | Evita alterações acidentais |

---

## Exemplo completo

```go
package main

import "fmt"

func main() {

    // Declaração de variáveis
    nome := "João"
    idade := 21
    altura := 1.80
    estudante := true

    // Constante
    const universidade = "Impacta"

    // Exibição formatada
    fmt.Printf("Nome: %s\n", nome)
    fmt.Printf("Idade: %d\n", idade)
    fmt.Printf("Altura: %.2f\n", altura)
    fmt.Printf("Estudante: %t\n", estudante)
    fmt.Printf("Universidade: %s\n", universidade)
}
```

---

## Próximos passos

Agora que já entendemos a sintaxe básica e o funcionamento das variáveis, o próximo passo é estudar as estruturas de controle da linguagem Go.

➡️ [Estruturas de Controle](03-estruturas.md)

---

## Resumo

Nesta página aprendemos:

- Estrutura básica de programas Go
- Comentários
- Declaração de variáveis
- Inferência de tipos
- Constantes
- Tipos primitivos
- Formatação de saída
- Convenções de nomenclatura
- Boas práticas

!!! note "Resumo Final"
    A sintaxe simples do Go é um dos principais motivos da popularidade da linguagem. Dominar variáveis e tipos primitivos é essencial para construir aplicações robustas e profissionais.
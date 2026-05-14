# Arrays, Slices e Maps

Coleções são estruturas utilizadas para armazenar múltiplos valores em uma única variável. Em Go, as principais coleções são:

- Arrays
- Slices
- Maps

Essas estruturas são fundamentais para manipular listas de dados, conjuntos de informações e estruturas dinâmicas.

---

## Arrays

Arrays são coleções de tamanho fixo que armazenam elementos do mesmo tipo.

### Sintaxe básica

```go
var nomeArray [tamanho]tipo
```

---

## Exemplo de Array

```go
package main

import "fmt"

func main() {

    var numeros [5]int

    numeros[0] = 10
    numeros[1] = 20
    numeros[2] = 30

    fmt.Println(numeros)
}
```

Resultado:

```text
[10 20 30 0 0]
```

---

## Inicializando Arrays

### Exemplo

```go
package main

import "fmt"

func main() {

    nomes := [3]string{"Ana", "Carlos", "Maria"}

    fmt.Println(nomes)
}
```

---

## Acessando posições do Array

Cada elemento possui um índice iniciado em `0`.

| Índice | Valor |
|---|---|
| `0` | Primeiro elemento |
| `1` | Segundo elemento |
| `2` | Terceiro elemento |

### Exemplo

```go
package main

import "fmt"

func main() {

    frutas := [3]string{"Maçã", "Banana", "Uva"}

    fmt.Println(frutas[0])
    fmt.Println(frutas[1])
}
```

---

## Descobrindo o tamanho do Array

Utilizamos a função `len()`.

### Exemplo

```go
package main

import "fmt"

func main() {

    numeros := [5]int{1, 2, 3, 4, 5}

    fmt.Println(len(numeros))
}
```

---

## Limitações dos Arrays

Arrays possuem tamanho fixo. Isso significa que não podem crescer dinamicamente.

!!! warning "Cuidado"
    Arrays são pouco utilizados em aplicações modernas Go. Na maioria dos casos, utiliza-se Slices.

---

# Slices

Slices são estruturas dinâmicas construídas sobre arrays.

Elas são muito mais flexíveis e amplamente utilizadas em Go.

---

## Criando um Slice

### Exemplo

```go
package main

import "fmt"

func main() {

    nomes := []string{"Pedro", "Ana", "Carlos"}

    fmt.Println(nomes)
}
```

---

## Diferença entre Array e Slice

| Estrutura | Tamanho fixo | Dinâmico |
|---|---|---|
| Array | ✅ | ❌ |
| Slice | ❌ | ✅ |

---

## Adicionando elementos com `append`

### Exemplo

```go
package main

import "fmt"

func main() {

    numeros := []int{1, 2, 3}

    numeros = append(numeros, 4)
    numeros = append(numeros, 5)

    fmt.Println(numeros)
}
```

---

## Percorrendo Slices com `for range`

### Exemplo

```go
package main

import "fmt"

func main() {

    frutas := []string{"Maçã", "Banana", "Uva"}

    for indice, valor := range frutas {

        fmt.Printf("Índice: %d | Valor: %s\n", indice, valor)
    }
}
```

---

## Criando Slice com `make`

A função `make()` permite criar slices com tamanho e capacidade definidos.

### Exemplo

```go
package main

import "fmt"

func main() {

    numeros := make([]int, 5)

    fmt.Println(numeros)
}
```

---

## Comprimento e capacidade

| Função | Descrição |
|---|---|
| `len()` | Quantidade de elementos |
| `cap()` | Capacidade total do slice |

### Exemplo

```go
package main

import "fmt"

func main() {

    numeros := make([]int, 3, 5)

    fmt.Println("Tamanho:", len(numeros))
    fmt.Println("Capacidade:", cap(numeros))
}
```

---

## Removendo elementos de um Slice

Go não possui função nativa para remoção, mas é possível manipular o slice.

### Exemplo

```go
package main

import "fmt"

func main() {

    numeros := []int{1, 2, 3, 4, 5}

    // Remove o índice 2
    numeros = append(numeros[:2], numeros[3:]...)

    fmt.Println(numeros)
}
```

!!! tip "Dica de Ouro"
    Slices são extremamente importantes em Go. Grande parte das aplicações utiliza slices constantemente.

---

# Maps

Maps são estruturas chave-valor semelhantes a dicionários ou objetos JSON.

---

## Criando um Map

### Exemplo

```go
package main

import "fmt"

func main() {

    usuario := map[string]string{
        "nome":  "Pedro",
        "email": "pedro@email.com",
    }

    fmt.Println(usuario)
}
```

---

## Acessando valores do Map

### Exemplo

```go
package main

import "fmt"

func main() {

    usuario := map[string]string{
        "nome": "Maria",
    }

    fmt.Println(usuario["nome"])
}
```

---

## Adicionando valores ao Map

### Exemplo

```go
package main

import "fmt"

func main() {

    usuario := make(map[string]string)

    usuario["nome"] = "Carlos"
    usuario["cidade"] = "São Paulo"

    fmt.Println(usuario)
}
```

---

## Removendo valores com `delete`

### Exemplo

```go
package main

import "fmt"

func main() {

    usuario := map[string]string{
        "nome":  "Pedro",
        "email": "pedro@email.com",
    }

    delete(usuario, "email")

    fmt.Println(usuario)
}
```

---

## Verificando se uma chave existe

### Exemplo

```go
package main

import "fmt"

func main() {

    usuario := map[string]string{
        "nome": "Ana",
    }

    valor, existe := usuario["nome"]

    fmt.Println(valor)
    fmt.Println(existe)
}
```

---

## Percorrendo Maps

### Exemplo

```go
package main

import "fmt"

func main() {

    usuario := map[string]string{
        "nome":  "Pedro",
        "cidade": "São Paulo",
    }

    for chave, valor := range usuario {

        fmt.Printf("%s: %s\n", chave, valor)
    }
}
```

---

## Comparação entre Arrays, Slices e Maps

| Estrutura | Uso principal | Dinâmico |
|---|---|---|
| Array | Dados fixos | ❌ |
| Slice | Listas dinâmicas | ✅ |
| Map | Estrutura chave-valor | ✅ |

---

## Boas práticas com coleções

| Boa prática | Motivo |
|---|---|
| Preferir Slices ao invés de Arrays | Maior flexibilidade |
| Utilizar Maps para buscas rápidas | Melhor organização |
| Evitar modificar slices durante loops complexos | Reduz erros |
| Utilizar `make()` quando possível | Melhor performance |

!!! note "Nota Importante"
    Slices e Maps são estruturas extremamente utilizadas em APIs, microsserviços e aplicações backend modernas.

---

## Exemplo completo

```go
package main

import "fmt"

func main() {

    // Slice
    linguagens := []string{"Go", "Python", "Java"}

    linguagens = append(linguagens, "Rust")

    // Map
    desenvolvedor := map[string]string{
        "nome": "Pedro",
        "cargo": "Backend Developer",
    }

    // Loop no slice
    for _, linguagem := range linguagens {

        fmt.Println(linguagem)
    }

    // Loop no map
    for chave, valor := range desenvolvedor {

        fmt.Printf("%s: %s\n", chave, valor)
    }
}
```

---

## Próximos passos

Agora que aprendemos a trabalhar com coleções de dados, o próximo passo é estudar Structs e Métodos em Go.

➡️ [Structs e Métodos](05-structs.md)

---

## Resumo

Nesta página aprendemos:

- Arrays
- Slices
- Maps
- Loops com `range`
- Uso de `append`
- Uso de `make`
- Manipulação de dados
- Estruturas chave-valor

!!! note "Resumo Final"
    Arrays, Slices e Maps são estruturas fundamentais para manipulação de dados em Go. Dominar essas coleções é essencial para desenvolver aplicações modernas, eficientes e escaláveis.
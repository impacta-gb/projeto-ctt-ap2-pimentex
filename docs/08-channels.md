# Channels

Os `Channels` são um dos recursos mais importantes da concorrência em Go.

Eles permitem a comunicação segura entre Goroutines, evitando problemas de sincronização e compartilhamento incorreto de memória.

A filosofia da linguagem Go é:

> "Não compartilhe memória entre Goroutines; compartilhe dados através de comunicação."

---

## O que é um Channel?

Um `Channel` é um mecanismo utilizado para enviar e receber dados entre Goroutines.

Ele funciona como um canal de comunicação.

---

## Criando um Channel

Utilizamos a função `make()`.

### Sintaxe básica

```go
canal := make(chan tipo)
```

---

## Exemplo simples de Channel

```go
package main

import "fmt"

func main() {

    canal := make(chan string)

    go func() {

        canal <- "Olá, Channel!"
    }()

    mensagem := <-canal

    fmt.Println(mensagem)
}
```

---

## Entendendo o exemplo

| Elemento | Função |
|---|---|
| `chan string` | Channel do tipo string |
| `canal <- valor` | Envia valor |
| `<-canal` | Recebe valor |

---

## Fluxo de comunicação

```text
Goroutine 1 ---> Channel ---> Goroutine 2
```

---

## Channels são bloqueantes

Por padrão:

- O envio aguarda alguém receber
- O recebimento aguarda alguém enviar

!!! note "Nota Importante"
    Channels ajudam a sincronizar Goroutines automaticamente.

---

## Exemplo de bloqueio

```go
package main

import "fmt"

func main() {

    canal := make(chan int)

    canal <- 10

    fmt.Println(<-canal)
}
```

!!! warning "Cuidado"
    O código acima gera deadlock porque ninguém está recebendo o valor enquanto ele é enviado.

---

# Buffered Channels

Channels com buffer permitem armazenar valores temporariamente.

---

## Criando Buffered Channel

### Sintaxe

```go
canal := make(chan int, capacidade)
```

---

## Exemplo com buffer

```go
package main

import "fmt"

func main() {

    canal := make(chan int, 2)

    canal <- 10
    canal <- 20

    fmt.Println(<-canal)
    fmt.Println(<-canal)
}
```

---

## Diferença entre Channel normal e Buffered

| Tipo | Bloqueante imediato |
|---|---|
| Channel normal | ✅ Sim |
| Buffered Channel | ❌ Não (até encher buffer) |

---

## Utilizando Goroutines com Channels

### Exemplo

```go
package main

import "fmt"

func processar(canal chan string) {

    canal <- "Processamento concluído"
}

func main() {

    canal := make(chan string)

    go processar(canal)

    mensagem := <-canal

    fmt.Println(mensagem)
}
```

---

# Direção de Channels

Go permite limitar canais para apenas envio ou recebimento.

---

## Channel somente envio

```go
chan<- string
```

---

## Channel somente recebimento

```go
<-chan string
```

---

## Exemplo completo

```go
package main

import "fmt"

// Somente envio
func enviar(canal chan<- string) {

    canal <- "Olá"
}

// Somente recebimento
func receber(canal <-chan string) {

    mensagem := <-canal

    fmt.Println(mensagem)
}

func main() {

    canal := make(chan string)

    go enviar(canal)

    receber(canal)
}
```

---

# Loop em Channels

Podemos percorrer Channels utilizando `range`.

---

## Exemplo com range

```go
package main

import "fmt"

func main() {

    canal := make(chan int)

    go func() {

        for i := 1; i <= 5; i++ {

            canal <- i
        }

        close(canal)
    }()

    for valor := range canal {

        fmt.Println(valor)
    }
}
```

---

# Fechando Channels

Utilizamos `close()` para indicar que não haverá mais envios.

---

## Exemplo

```go
close(canal)
```

---

## Verificando se o Channel foi fechado

### Exemplo

```go
package main

import "fmt"

func main() {

    canal := make(chan int)

    go func() {

        canal <- 10

        close(canal)
    }()

    valor, aberto := <-canal

    fmt.Println(valor)
    fmt.Println(aberto)
}
```

---

## Entendendo retorno do Channel

| Valor | Significado |
|---|---|
| `true` | Channel aberto |
| `false` | Channel fechado |

---

# Select

O `select` permite aguardar múltiplos Channels simultaneamente.

---

## Exemplo com Select

```go
package main

import (
    "fmt"
    "time"
)

func main() {

    canal1 := make(chan string)
    canal2 := make(chan string)

    go func() {

        time.Sleep(time.Second)

        canal1 <- "Resposta do canal 1"
    }()

    go func() {

        time.Sleep(time.Second * 2)

        canal2 <- "Resposta do canal 2"
    }()

    select {

    case mensagem1 := <-canal1:
        fmt.Println(mensagem1)

    case mensagem2 := <-canal2:
        fmt.Println(mensagem2)
    }
}
```

---

## Entendendo o Select

| Recurso | Função |
|---|---|
| `select` | Aguarda múltiplos canais |
| `case` | Executa canal disponível |
| `default` | Executa se nenhum canal responder |

---

## Exemplo com Default

```go
package main

import "fmt"

func main() {

    canal := make(chan string)

    select {

    case mensagem := <-canal:
        fmt.Println(mensagem)

    default:
        fmt.Println("Nenhuma mensagem disponível")
    }
}
```

---

# Deadlock

Deadlock ocorre quando Goroutines ficam bloqueadas esperando umas pelas outras.

---

## Exemplo de Deadlock

```go
package main

func main() {

    canal := make(chan int)

    canal <- 1
}
```

Resultado:

```text
fatal error: all goroutines are asleep - deadlock!
```

!!! warning "Cuidado"
    Deadlocks são um dos erros mais comuns ao trabalhar com Channels.

---

## Boas práticas com Channels

| Boa prática | Motivo |
|---|---|
| Fechar canais corretamente | Evita vazamentos |
| Utilizar `select` | Melhor controle |
| Evitar deadlocks | Código mais seguro |
| Utilizar buffered channels quando necessário | Melhor performance |

!!! tip "Dica de Ouro"
    Channels são a forma mais idiomática de comunicação concorrente em Go.

---

## Comparação entre Mutex e Channels

| Recurso | Melhor uso |
|---|---|
| Mutex | Compartilhamento de memória |
| Channels | Comunicação entre Goroutines |

---

## Exemplo completo

```go
package main

import (
    "fmt"
    "time"
)

func worker(id int, canal chan string) {

    time.Sleep(time.Second)

    canal <- fmt.Sprintf("Worker %d finalizado", id)
}

func main() {

    canal := make(chan string)

    for i := 1; i <= 3; i++ {

        go worker(i, canal)
    }

    for i := 1; i <= 3; i++ {

        mensagem := <-canal

        fmt.Println(mensagem)
    }
}
```

---

## Próximos passos

Agora que aprendemos concorrência com Channels, o próximo passo é estudar gerenciamento de dependências utilizando Go Modules.

➡️ [Go Modules](09-gomodules.md)

---

## Resumo

Nesta página aprendemos:

- O que são Channels
- Comunicação entre Goroutines
- Buffered Channels
- Select
- Deadlocks
- Fechamento de canais
- Comunicação concorrente
- Sincronização automática

!!! note "Resumo Final"
    Channels são um dos recursos mais poderosos da linguagem Go. Eles tornam a concorrência mais segura, organizada e eficiente, permitindo criar aplicações altamente escaláveis e modernas.
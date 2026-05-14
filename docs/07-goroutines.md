# Goroutines

Uma das maiores vantagens da linguagem Go é seu poderoso sistema de concorrência nativa.

As `Goroutines` permitem executar múltiplas tarefas simultaneamente de forma leve, rápida e eficiente.

Essa funcionalidade tornou Go extremamente popular em aplicações:

- Cloud Computing
- APIs REST
- Microsserviços
- Sistemas distribuídos
- Processamento paralelo
- Ferramentas DevOps

---

## O que é concorrência?

Concorrência é a capacidade de executar múltiplas tarefas ao mesmo tempo.

Em aplicações modernas, isso é essencial para melhorar:

- Performance
- Escalabilidade
- Utilização de recursos
- Tempo de resposta

---

## O que é uma Goroutine?

Uma Goroutine é uma função executada concorrentemente.

Ela é muito mais leve que uma thread tradicional do sistema operacional.

### Sintaxe básica

```go
go minhaFuncao()
```

---

## Primeiro exemplo com Goroutine

### Exemplo

```go
package main

import (
    "fmt"
    "time"
)

func mensagem() {

    fmt.Println("Executando Goroutine")
}

func main() {

    go mensagem()

    time.Sleep(time.Second)
}
```

---

## Entendendo o exemplo

| Elemento | Função |
|---|---|
| `go` | Executa função concorrentemente |
| `time.Sleep()` | Aguarda execução da Goroutine |
| `main()` | Função principal do programa |

!!! note "Nota Importante"
    Quando a função `main()` termina, todas as Goroutines são encerradas automaticamente.

---

## Executando múltiplas Goroutines

### Exemplo

```go
package main

import (
    "fmt"
    "time"
)

func tarefa(nome string) {

    for i := 1; i <= 3; i++ {

        fmt.Println(nome, "-", i)

        time.Sleep(time.Millisecond * 500)
    }
}

func main() {

    go tarefa("Goroutine 1")
    go tarefa("Goroutine 2")

    time.Sleep(time.Second * 3)
}
```

---

## Goroutines são leves

Diferente de threads tradicionais, Goroutines consomem pouca memória.

| Tecnologia | Consumo aproximado |
|---|---|
| Thread tradicional | MBs |
| Goroutine | KBs |

!!! tip "Dica de Ouro"
    Aplicações Go conseguem executar milhares de Goroutines simultaneamente com excelente performance.

---

## Funções anônimas com Goroutines

Também é possível utilizar funções anônimas.

### Exemplo

```go
package main

import (
    "fmt"
    "time"
)

func main() {

    go func() {

        fmt.Println("Executando função anônima")
    }()

    time.Sleep(time.Second)
}
```

---

## Problema de sincronização

Em aplicações concorrentes, múltiplas Goroutines podem acessar o mesmo recurso ao mesmo tempo.

Isso pode gerar:

- Race Conditions
- Dados inconsistentes
- Bugs difíceis de identificar

---

## Exemplo de Race Condition

### Exemplo

```go
package main

import (
    "fmt"
    "time"
)

var contador int

func incrementar() {

    for i := 0; i < 1000; i++ {

        contador++
    }
}

func main() {

    go incrementar()
    go incrementar()

    time.Sleep(time.Second)

    fmt.Println(contador)
}
```

!!! warning "Cuidado"
    O resultado pode variar devido ao acesso concorrente não controlado.

---

# WaitGroup

O `WaitGroup` permite aguardar a finalização das Goroutines.

---

## Exemplo com WaitGroup

```go
package main

import (
    "fmt"
    "sync"
)

func tarefa(nome string, wg *sync.WaitGroup) {

    defer wg.Done()

    fmt.Println(nome)
}

func main() {

    var wg sync.WaitGroup

    wg.Add(2)

    go tarefa("Goroutine 1", &wg)
    go tarefa("Goroutine 2", &wg)

    wg.Wait()

    fmt.Println("Finalizado")
}
```

---

## Entendendo o WaitGroup

| Método | Função |
|---|---|
| `Add()` | Adiciona Goroutines |
| `Done()` | Finaliza uma Goroutine |
| `Wait()` | Aguarda todas terminarem |

---

## Mutex

O `Mutex` evita acessos simultâneos a recursos compartilhados.

---

## Exemplo com Mutex

```go
package main

import (
    "fmt"
    "sync"
)

var contador int
var mutex sync.Mutex

func incrementar(wg *sync.WaitGroup) {

    defer wg.Done()

    for i := 0; i < 1000; i++ {

        mutex.Lock()

        contador++

        mutex.Unlock()
    }
}

func main() {

    var wg sync.WaitGroup

    wg.Add(2)

    go incrementar(&wg)
    go incrementar(&wg)

    wg.Wait()

    fmt.Println(contador)
}
```

---

## Entendendo o Mutex

| Método | Função |
|---|---|
| `Lock()` | Bloqueia acesso |
| `Unlock()` | Libera acesso |

!!! note "Nota Importante"
    Mutex é fundamental para evitar Race Conditions em aplicações concorrentes.

---

## Scheduler do Go

O Go possui um scheduler interno responsável por gerenciar Goroutines automaticamente.

Ele distribui as tarefas entre múltiplos núcleos do processador.

---

## Vantagens das Goroutines

| Vantagem | Benefício |
|---|---|
| Leves | Baixo consumo de memória |
| Rápidas | Excelente performance |
| Escaláveis | Milhares simultâneas |
| Simples | Fácil implementação |

---

## Quando utilizar Goroutines

Goroutines são muito úteis em:

- Requisições HTTP
- Processamento paralelo
- Uploads simultâneos
- APIs REST
- Workers
- Filas
- Streaming

---

## Boas práticas com Goroutines

| Boa prática | Motivo |
|---|---|
| Utilizar WaitGroup | Melhor sincronização |
| Evitar Race Conditions | Código mais seguro |
| Utilizar Mutex quando necessário | Proteção de dados |
| Evitar Goroutines desnecessárias | Melhor controle |

!!! warning "Cuidado"
    Criar Goroutines sem controle pode gerar vazamentos de memória e problemas de performance.

---

## Exemplo completo

```go
package main

import (
    "fmt"
    "sync"
)

func processar(id int, wg *sync.WaitGroup) {

    defer wg.Done()

    fmt.Printf("Processando tarefa %d\n", id)
}

func main() {

    var wg sync.WaitGroup

    for i := 1; i <= 5; i++ {

        wg.Add(1)

        go processar(i, &wg)
    }

    wg.Wait()

    fmt.Println("Todas as tarefas finalizadas")
}
```

---

## Próximos passos

Agora que aprendemos concorrência com Goroutines, o próximo passo é estudar comunicação entre Goroutines utilizando Channels.

➡️ [Channels](08-channels.md)

---

## Resumo

Nesta página aprendemos:

- O que são Goroutines
- Execução concorrente
- Concorrência em Go
- WaitGroup
- Mutex
- Race Conditions
- Scheduler do Go
- Sincronização de tarefas

!!! note "Resumo Final"
    Goroutines são um dos recursos mais poderosos da linguagem Go. Elas permitem criar aplicações altamente concorrentes, escaláveis e eficientes com muito menos complexidade que outras linguagens.
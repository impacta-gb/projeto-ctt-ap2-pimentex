# Tratamento de Erros

O tratamento de erros é uma das características mais importantes da linguagem Go.

Diferente de muitas linguagens modernas que utilizam exceções (`try/catch`), Go utiliza uma abordagem explícita baseada no tipo `error`.

Essa filosofia torna o código mais previsível, simples e fácil de manter.

---

## O que é um erro em Go?

Em Go, erros são valores que podem ser retornados por funções.

O tipo padrão utilizado é:

```go
error
```

---

## Estrutura padrão de tratamento de erros

Em Go, normalmente uma função retorna:

- O resultado esperado
- Um erro

### Exemplo de sintaxe

```go
resultado, err := minhaFuncao()
```

---

## Primeiro exemplo com erro

### Exemplo

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {

    numero, err := strconv.Atoi("123")

    if err != nil {

        fmt.Println("Erro ao converter valor")
        return
    }

    fmt.Println(numero)
}
```

---

## Entendendo o `err != nil`

| Expressão | Significado |
|---|---|
| `err == nil` | Nenhum erro ocorreu |
| `err != nil` | Um erro aconteceu |

!!! note "Nota Importante"
    Em Go, sempre devemos verificar erros retornados por funções importantes.

---

## Exemplo com erro real

### Exemplo

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {

    numero, err := strconv.Atoi("abc")

    if err != nil {

        fmt.Println("Erro encontrado:")
        fmt.Println(err)

        return
    }

    fmt.Println(numero)
}
```

Resultado:

```text
strconv.Atoi: parsing "abc": invalid syntax
```

---

## Ignorando erros com `_`

O caractere `_` ignora valores retornados.

### Exemplo

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {

    numero, _ := strconv.Atoi("100")

    fmt.Println(numero)
}
```

!!! warning "Cuidado"
    Ignorar erros pode gerar comportamentos inesperados e dificultar a manutenção do sistema.

---

## Criando erros personalizados

A biblioteca `errors` permite criar mensagens de erro personalizadas.

### Exemplo

```go
package main

import (
    "errors"
    "fmt"
)

func dividir(a, b float64) (float64, error) {

    if b == 0 {

        return 0, errors.New("não é possível dividir por zero")
    }

    return a / b, nil
}

func main() {

    resultado, err := dividir(10, 0)

    if err != nil {

        fmt.Println("Erro:", err)
        return
    }

    fmt.Println(resultado)
}
```

---

## Retornando múltiplos valores

Go permite retornar múltiplos valores em funções.

### Exemplo

```go
package main

import "fmt"

func soma(a int, b int) (int, error) {

    resultado := a + b

    return resultado, nil
}

func main() {

    resultado, err := soma(10, 5)

    if err != nil {

        fmt.Println(err)
        return
    }

    fmt.Println(resultado)
}
```

---

## Boas práticas no tratamento de erros

| Boa prática | Motivo |
|---|---|
| Sempre verificar `err` | Evita falhas inesperadas |
| Retornar erros claros | Facilita depuração |
| Não ignorar erros sem necessidade | Código mais seguro |
| Utilizar mensagens objetivas | Melhor manutenção |

---

## Encadeamento de erros

Em sistemas maiores, funções podem propagar erros.

### Exemplo

```go
package main

import (
    "errors"
    "fmt"
)

func buscarUsuario(id int) (string, error) {

    if id == 0 {

        return "", errors.New("usuário não encontrado")
    }

    return "Pedro", nil
}

func processarUsuario(id int) error {

    usuario, err := buscarUsuario(id)

    if err != nil {

        return err
    }

    fmt.Println(usuario)

    return nil
}

func main() {

    err := processarUsuario(0)

    if err != nil {

        fmt.Println("Erro:", err)
    }
}
```

---

# Panic

O `panic` interrompe imediatamente a execução do programa.

Ele deve ser utilizado apenas em situações críticas.

---

## Exemplo de Panic

```go
package main

func main() {

    panic("erro crítico no sistema")
}
```

!!! warning "Cuidado"
    O uso excessivo de `panic` não é recomendado. Em aplicações profissionais, prefira tratamento de erros tradicionais.

---

# Recover

O `recover` permite capturar um `panic`.

---

## Exemplo com Recover

```go
package main

import "fmt"

func main() {

    defer func() {

        if r := recover(); r != nil {

            fmt.Println("Erro recuperado:")
            fmt.Println(r)
        }
    }()

    panic("falha inesperada")
}
```

---

## Entendendo `defer`

O `defer` agenda uma função para ser executada ao final da execução atual.

### Exemplo

```go
package main

import "fmt"

func main() {

    defer fmt.Println("Finalizando programa")

    fmt.Println("Executando...")
}
```

Resultado:

```text
Executando...
Finalizando programa
```

---

## Quando utilizar `panic`

| Situação | Recomendado? |
|---|---|
| Erros comuns | ❌ Não |
| Arquivos inexistentes | ❌ Não |
| Falhas críticas irreversíveis | ✅ Sim |
| Erros de inicialização do sistema | ✅ Sim |

---

## Comparação entre Error e Panic

| Estrutura | Uso |
|---|---|
| `error` | Tratamento normal |
| `panic` | Falhas críticas |
| `recover` | Recuperação de panic |

---

## Exemplo completo

```go
package main

import (
    "errors"
    "fmt"
)

func sacar(saldo float64, valor float64) (float64, error) {

    if valor > saldo {

        return saldo, errors.New("saldo insuficiente")
    }

    saldo -= valor

    return saldo, nil
}

func main() {

    saldoAtual, err := sacar(100, 150)

    if err != nil {

        fmt.Println("Erro:", err)
        return
    }

    fmt.Println("Novo saldo:", saldoAtual)
}
```

---

## Tratamento de erros em aplicações reais

Em aplicações modernas, o tratamento de erros é essencial em:

- APIs REST
- Banco de dados
- Sistemas distribuídos
- Microsserviços
- Integrações externas
- Operações de arquivos

!!! tip "Dica de Ouro"
    Sistemas robustos tratam erros corretamente em todas as camadas da aplicação.

---

## Próximos passos

Agora que aprendemos como tratar erros em Go, o próximo passo é estudar concorrência utilizando Goroutines.

➡️ [Goroutines](07-goroutines.md)

---

## Resumo

Nesta página aprendemos:

- O tipo `error`
- Verificação com `err != nil`
- Criação de erros personalizados
- Encadeamento de erros
- Uso de `panic`
- Uso de `recover`
- Uso de `defer`
- Boas práticas

!!! note "Resumo Final"
    O tratamento explícito de erros é uma das principais características do Go. Essa abordagem torna aplicações mais previsíveis, robustas e fáceis de manter em ambientes profissionais.
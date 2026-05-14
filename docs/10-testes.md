# Testes Automatizados em Go

Os testes automatizados são fundamentais no desenvolvimento moderno de software.

Eles permitem validar o funcionamento da aplicação, reduzir bugs e garantir maior segurança durante alterações no código.

A linguagem Go possui um sistema de testes nativo, simples e extremamente eficiente.

---

## Por que testar aplicações?

Testes ajudam a:

- Detectar erros rapidamente
- Garantir qualidade
- Facilitar manutenção
- Evitar regressões
- Melhorar confiabilidade

---

## Biblioteca de testes do Go

Go possui suporte nativo através do pacote:

```go
testing
```

Não é necessário instalar bibliotecas externas para criar testes básicos.

---

## Estrutura de arquivos de teste

Arquivos de teste devem terminar com:

```text
_test.go
```

---

## Exemplo de estrutura

```text
projeto/
├── calculadora.go
└── calculadora_test.go
```

---

# Criando a primeira função

## Arquivo `calculadora.go`

```go
package main

// Função de soma
func Somar(a int, b int) int {

    return a + b
}
```

---

# Criando o primeiro teste

## Arquivo `calculadora_test.go`

```go
package main

import "testing"

// Função de teste
func TestSomar(t *testing.T) {

    resultado := Somar(10, 5)

    esperado := 15

    if resultado != esperado {

        t.Errorf("Esperado %d, mas recebeu %d", esperado, resultado)
    }
}
```

---

## Entendendo a estrutura do teste

| Elemento | Função |
|---|---|
| `TestSomar` | Nome do teste |
| `t *testing.T` | Controle do teste |
| `t.Errorf()` | Exibe erro no teste |

---

## Executando testes

### Comando

```bash
go test
```

---

## Resultado de sucesso

```text
PASS
ok      projeto    0.001s
```

---

## Resultado com falha

```text
--- FAIL: TestSomar
Esperado 15, mas recebeu 10
FAIL
```

!!! note "Nota Importante"
    Todo teste em Go deve começar com a palavra `Test`.

---

# Testando múltiplos cenários

---

## Exemplo

```go
package main

import "testing"

func TestSubtrair(t *testing.T) {

    testes := []struct {
        nome      string
        a         int
        b         int
        esperado  int
    }{
        {"Teste 1", 10, 5, 5},
        {"Teste 2", 20, 10, 10},
        {"Teste 3", 50, 25, 25},
    }

    for _, teste := range testes {

        resultado := teste.a - teste.b

        if resultado != teste.esperado {

            t.Errorf(
                "%s falhou: esperado %d, recebeu %d",
                teste.nome,
                teste.esperado,
                resultado,
            )
        }
    }
}
```

---

# Benchmark Tests

Benchmarks medem performance do código.

---

## Exemplo de benchmark

```go
package main

import "testing"

func BenchmarkSomar(b *testing.B) {

    for i := 0; i < b.N; i++ {

        Somar(10, 5)
    }
}
```

---

## Executando benchmark

```bash
go test -bench=.
```

---

## Resultado

```text
BenchmarkSomar-8    1000000000    0.25 ns/op
```

---

# Testes Verbosos

Para visualizar detalhes da execução:

```bash
go test -v
```

---

# Coverage (Cobertura de testes)

A cobertura indica quanto do código foi testado.

---

## Executando coverage

```bash
go test -cover
```

---

## Resultado

```text
coverage: 85.0% of statements
```

---

## Gerando relatório completo

```bash
go test -coverprofile=coverage.out
```

---

## Visualizando relatório HTML

```bash
go tool cover -html=coverage.out
```

!!! tip "Dica de Ouro"
    Cobertura alta não garante ausência de bugs, mas ajuda a identificar partes não testadas do sistema.

---

# Testes com Setup

Em projetos maiores, frequentemente precisamos preparar ambiente antes dos testes.

---

## Exemplo

```go
package main

import (
    "fmt"
    "testing"
)

func setup() {

    fmt.Println("Inicializando ambiente")
}

func TestExemplo(t *testing.T) {

    setup()

    resultado := 2 + 2

    if resultado != 4 {

        t.Error("Erro no cálculo")
    }
}
```

---

# Testes Paralelos

Go permite executar testes simultaneamente.

---

## Exemplo

```go
package main

import "testing"

func TestParalelo(t *testing.T) {

    t.Parallel()

    resultado := 1 + 1

    if resultado != 2 {

        t.Error("Erro")
    }
}
```

---

# Testando erros

Também podemos validar erros retornados pelas funções.

---

## Exemplo

```go
package main

import (
    "errors"
    "testing"
)

func Dividir(a float64, b float64) (float64, error) {

    if b == 0 {

        return 0, errors.New("divisão por zero")
    }

    return a / b, nil
}

func TestDividir(t *testing.T) {

    _, err := Dividir(10, 0)

    if err == nil {

        t.Error("Esperava erro de divisão por zero")
    }
}
```

---

# Tabela de principais comandos

| Comando | Função |
|---|---|
| `go test` | Executa testes |
| `go test -v` | Modo verboso |
| `go test -cover` | Mostra cobertura |
| `go test -bench=.` | Executa benchmarks |

---

# Boas práticas em testes

| Boa prática | Motivo |
|---|---|
| Criar testes pequenos | Melhor manutenção |
| Testar casos extremos | Maior segurança |
| Utilizar nomes claros | Melhor leitura |
| Automatizar testes | Mais produtividade |

!!! warning "Cuidado"
    Testes frágeis ou mal escritos podem gerar falsos positivos e dificultar manutenção.

---

# Estrutura profissional de testes

```text
projeto/
├── go.mod
├── main.go
├── services/
├── repositories/
├── handlers/
└── tests/
```

---

# Exemplo completo

## Arquivo `math.go`

```go
package main

func Multiplicar(a int, b int) int {

    return a * b
}
```

---

## Arquivo `math_test.go`

```go
package main

import "testing"

func TestMultiplicar(t *testing.T) {

    resultado := Multiplicar(5, 2)

    esperado := 10

    if resultado != esperado {

        t.Errorf(
            "Esperado %d, mas recebeu %d",
            esperado,
            resultado,
        )
    }
}
```

---

## Executando

```bash
go test -v
```

---

## Resultado esperado

```text
=== RUN   TestMultiplicar
--- PASS: TestMultiplicar (0.00s)
PASS
```

---

# Integração Contínua e Testes

Testes automatizados são extremamente utilizados em:

- CI/CD
- DevOps
- GitHub Actions
- GitLab CI
- Jenkins
- Microsserviços

!!! tip "Dica de Ouro"
    Em ambientes profissionais, testes automatizados são executados automaticamente a cada alteração no código.

---

# Próximos passos

Parabéns! 🎉

Você concluiu os principais fundamentos da linguagem Go utilizados no desenvolvimento moderno.

Agora você já possui base para avançar em:

- APIs REST
- Microsserviços
- Cloud Computing
- DevOps
- Docker
- Kubernetes
- Sistemas distribuídos

➡️ [Introdução e Instalação](01-intro.md)

---

# Resumo

Nesta página aprendemos:

- Como criar testes
- Estrutura `_test.go`
- Uso do pacote `testing`
- Benchmarks
- Coverage
- Testes paralelos
- Testes de erro
- Boas práticas

!!! note "Resumo Final"
    Testes automatizados são essenciais para criar aplicações confiáveis, escaláveis e profissionais. O Go oferece um sistema de testes simples, rápido e extremamente poderoso integrado diretamente à linguagem.
# Testes Automatizados em Go

## Introdução aos Testes em Go

Os testes automatizados são uma das práticas mais importantes no desenvolvimento moderno de software. A linguagem Go possui suporte nativo para testes através do pacote `testing`, permitindo validar funcionalidades de forma simples, rápida e eficiente.

Ao criar testes automatizados, conseguimos:

- Garantir que o código funciona corretamente
- Detectar erros rapidamente
- Facilitar manutenção futura
- Melhorar a confiabilidade da aplicação
- Integrar testes em pipelines de CI/CD

!!! note "Nota Importante"
    Em Go, os testes fazem parte da própria linguagem e não exigem frameworks externos para funcionalidades básicas.

---

## Estrutura de Arquivos de Teste

Os testes em Go seguem uma convenção específica de nomenclatura.

Todo arquivo de teste deve terminar com o sufixo `_test.go`.

### Exemplo de Estrutura

| Arquivo | Função |
|---|---|
| `calculadora.go` | Código principal |
| `calculadora_test.go` | Arquivo contendo os testes |

---

## Criando o Primeiro Teste

Vamos criar uma função simples de soma e validar seu comportamento utilizando testes automatizados.

### Arquivo Principal

```go
package calculadora

// Soma retorna a soma de dois números inteiros.
func Soma(a int, b int) int {
	return a + b
}
```

---

### Arquivo de Teste

```go
package calculadora

import "testing"

// TestSoma verifica se a função Soma retorna o valor esperado.
func TestSoma(t *testing.T) {
	resultado := Soma(2, 3)

	esperado := 5

	if resultado != esperado {
		t.Errorf("Esperado %d, mas recebeu %d", esperado, resultado)
	}
}
```

!!! tip "Dica de Ouro"
    Os nomes das funções de teste devem começar obrigatoriamente com `Test` para que o Go consiga identificá-las automaticamente.

---

## Executando Testes

O Go oferece comandos simples para execução dos testes diretamente pelo terminal.

### Executar testes do diretório atual

```bash
go test
```

### Executar todos os testes do projeto

```bash
go test ./...
```

### Executar testes com detalhes adicionais

```bash
go test -v
```

---

## Principais Comandos de Teste

| Comando | Descrição |
|---|---|
| `go test` | Executa testes do diretório atual |
| `go test ./...` | Executa todos os testes do projeto |
| `go test -v` | Mostra saída detalhada |
| `go test -cover` | Exibe cobertura de testes |
| `go test -run TestNome` | Executa um teste específico |

---

## Cobertura de Testes

A cobertura de testes mede quanto do código foi executado durante os testes automatizados.

### Executando análise de cobertura

```bash
go test -cover
```

### Exemplo de saída

```text
coverage: 85.7% of statements
```

!!! warning "Cuidado"
    Alta cobertura de testes não garante ausência de bugs. O mais importante é testar cenários relevantes e críticos da aplicação.

---

## Testes com Múltiplos Cenários

Uma prática muito comum em Go é utilizar testes baseados em tabelas (Table Driven Tests).

Essa abordagem facilita manutenção e reduz repetição de código.

### Exemplo de Teste com Tabela

```go
package calculadora

import "testing"

// TestSomaTabela executa múltiplos cenários de teste.
func TestSomaTabela(t *testing.T) {

	testes := []struct {
		nome      string
		a         int
		b         int
		esperado  int
	}{
		{
			nome: "Soma positiva",
			a: 2,
			b: 3,
			esperado: 5,
		},
		{
			nome: "Soma com negativo",
			a: -1,
			b: 1,
			esperado: 0,
		},
		{
			nome: "Soma com zero",
			a: 0,
			b: 5,
			esperado: 5,
		},
	}

	for _, teste := range testes {

		resultado := Soma(teste.a, teste.b)

		if resultado != teste.esperado {
			t.Errorf(
				"%s: esperado %d, recebeu %d",
				teste.nome,
				teste.esperado,
				resultado,
			)
		}
	}
}
```

---

## Benchmarks em Go

Benchmarks são utilizados para medir desempenho e eficiência do código.

As funções de benchmark devem começar com `Benchmark`.

### Exemplo de Benchmark

```go
package calculadora

import "testing"

// BenchmarkSoma mede desempenho da função Soma.
func BenchmarkSoma(b *testing.B) {

	for i := 0; i < b.N; i++ {
		Soma(10, 20)
	}
}
```

### Executando Benchmarks

```bash
go test -bench=.
```

---

## Boas Práticas para Testes

| Boa Prática | Benefício |
|---|---|
| Criar testes pequenos | Facilita manutenção |
| Testar cenários de erro | Aumenta confiabilidade |
| Usar nomes descritivos | Melhora legibilidade |
| Automatizar execução | Integra facilmente com CI/CD |
| Evitar dependência entre testes | Reduz falhas inesperadas |

!!! tip "Dica de Ouro"
    Testes devem ser rápidos, independentes e previsíveis. Um teste lento ou instável reduz a confiança no projeto.

---

## Integração com CI/CD

Os testes automatizados são essenciais em pipelines de Integração Contínua (CI).

No projeto CTT-AP2, os testes e validações são executados automaticamente através do GitHub Actions durante:

- Pull Requests
- Pushes na branch `main`
- Execuções agendadas (`schedule`)

Esse processo garante que alterações sejam verificadas antes da publicação do site.

### Fluxo Simplificado do Pipeline

| Evento | Ação Executada |
|---|---|
| Pull Request | Validação do projeto |
| Push na `main` | Build e deploy |
| Schedule | Execução automática semanal |

!!! note "Nota Importante"
    A automação de testes é uma das principais práticas utilizadas em ambientes DevOps e pipelines modernos de CI/CD.

---

## Relação com Outros Tópicos

| Tema | Link |
|---|---|
| Tratamento de Erros | [06-erros.md](06-erros.md) |
| Goroutines | [07-goroutines.md](07-goroutines.md) |
| Channels | [08-channels.md](08-channels.md) |
| Go Modules | [09-gomodules.md](09-gomodules.md) |

---

## Conclusão

Os testes automatizados são fundamentais para garantir qualidade, estabilidade e segurança em aplicações Go.

A simplicidade do pacote `testing`, combinada com a velocidade da linguagem Go, torna o processo de criação e execução de testes extremamente eficiente.

Além disso, a integração natural com pipelines de CI/CD facilita automação, validação contínua e entrega segura de software em ambientes profissionais.s
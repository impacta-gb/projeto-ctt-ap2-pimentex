# Structs e Métodos

Em Go, `structs` são utilizadas para agrupar diferentes tipos de dados em uma única estrutura organizada.

Já os métodos permitem adicionar comportamentos a essas estruturas, aproximando Go dos conceitos de programação orientada a objetos.

Structs são extremamente utilizadas no desenvolvimento de APIs, sistemas backend, microsserviços e aplicações cloud-native.

---

## O que é uma Struct?

Uma `struct` é uma estrutura composta que agrupa múltiplos campos relacionados.

### Sintaxe básica

```go
type NomeStruct struct {
    Campo tipo
}
```

---

## Criando uma Struct

### Exemplo

```go
package main

import "fmt"

// Definição da struct
type Usuario struct {
    Nome  string
    Idade int
}

func main() {

    // Criando um objeto da struct
    usuario := Usuario{
        Nome:  "Pedro",
        Idade: 22,
    }

    fmt.Println(usuario)
}
```

---

## Acessando campos da Struct

Utilizamos o operador `.` para acessar os atributos.

### Exemplo

```go
package main

import "fmt"

type Produto struct {
    Nome  string
    Preco float64
}

func main() {

    produto := Produto{
        Nome:  "Notebook",
        Preco: 4500.00,
    }

    fmt.Println(produto.Nome)
    fmt.Println(produto.Preco)
}
```

---

## Alterando valores da Struct

### Exemplo

```go
package main

import "fmt"

type Pessoa struct {
    Nome string
}

func main() {

    pessoa := Pessoa{
        Nome: "Carlos",
    }

    pessoa.Nome = "João"

    fmt.Println(pessoa.Nome)
}
```

---

## Struct sem valores iniciais

Go aplica automaticamente os chamados `zero values`.

### Exemplo

```go
package main

import "fmt"

type Usuario struct {
    Nome  string
    Idade int
}

func main() {

    var usuario Usuario

    fmt.Println(usuario)
}
```

Resultado:

```text
{ 0}
```

---

## Comparação entre tipos de dados

| Estrutura | Objetivo |
|---|---|
| Variável | Armazenar um valor |
| Array/Slice | Armazenar listas |
| Map | Estrutura chave-valor |
| Struct | Representar entidades complexas |

---

# Métodos em Go

Métodos são funções associadas a uma struct.

Eles permitem adicionar comportamentos personalizados aos objetos.

---

## Criando um método

### Sintaxe

```go
func (variavel Tipo) metodo() {
    // código
}
```

---

## Exemplo simples de método

```go
package main

import "fmt"

type Usuario struct {
    Nome string
}

// Método associado à struct Usuario
func (u Usuario) Saudacao() {

    fmt.Printf("Olá, %s!\n", u.Nome)
}

func main() {

    usuario := Usuario{
        Nome: "Pedro",
    }

    usuario.Saudacao()
}
```

---

## Receiver

O valor entre parênteses no método é chamado de `receiver`.

### Exemplo

```go
func (u Usuario) Saudacao()
```

| Elemento | Significado |
|---|---|
| `u` | Variável da struct |
| `Usuario` | Tipo associado |
| `Saudacao()` | Método |

---

## Métodos com retorno

Métodos também podem retornar valores.

### Exemplo

```go
package main

import "fmt"

type Produto struct {
    Nome  string
    Preco float64
}

// Método que retorna valor
func (p Produto) Desconto() float64 {

    return p.Preco * 0.9
}

func main() {

    produto := Produto{
        Nome:  "Monitor",
        Preco: 2000,
    }

    fmt.Println(produto.Desconto())
}
```

---

## Métodos com parâmetros

### Exemplo

```go
package main

import "fmt"

type Conta struct {
    Saldo float64
}

func (c Conta) Depositar(valor float64) float64 {

    return c.Saldo + valor
}

func main() {

    conta := Conta{
        Saldo: 100,
    }

    novoSaldo := conta.Depositar(50)

    fmt.Println(novoSaldo)
}
```

---

# Ponteiros em Métodos

Quando queremos modificar diretamente os dados da struct, utilizamos ponteiros.

---

## Método com ponteiro

### Exemplo

```go
package main

import "fmt"

type Conta struct {
    Saldo float64
}

// Ponteiro para alterar o valor original
func (c *Conta) Depositar(valor float64) {

    c.Saldo += valor
}

func main() {

    conta := Conta{
        Saldo: 100,
    }

    conta.Depositar(50)

    fmt.Println(conta.Saldo)
}
```

!!! note "Nota Importante"
    Métodos com ponteiros alteram o valor original da struct na memória.

---

## Diferença entre receiver normal e ponteiro

| Tipo | Altera valor original? |
|---|---|
| `(u Usuario)` | ❌ Não |
| `(u *Usuario)` | ✅ Sim |

---

## Structs aninhadas

Uma struct pode conter outra struct.

### Exemplo

```go
package main

import "fmt"

type Endereco struct {
    Cidade string
    Estado string
}

type Usuario struct {
    Nome     string
    Endereco Endereco
}

func main() {

    usuario := Usuario{
        Nome: "Pedro",
        Endereco: Endereco{
            Cidade: "São Paulo",
            Estado: "SP",
        },
    }

    fmt.Println(usuario)
}
```

---

## Structs anônimas

Go permite criar structs sem definir um tipo separado.

### Exemplo

```go
package main

import "fmt"

func main() {

    usuario := struct {
        Nome string
        Idade int
    }{
        Nome: "Maria",
        Idade: 30,
    }

    fmt.Println(usuario)
}
```

---

## Boas práticas com Structs

| Boa prática | Motivo |
|---|---|
| Utilizar nomes claros | Melhor legibilidade |
| Separar responsabilidades | Código mais organizado |
| Utilizar métodos para comportamentos | Facilita manutenção |
| Usar ponteiros quando necessário | Melhor performance |

!!! tip "Dica de Ouro"
    Structs são a base de grande parte das aplicações Go modernas, principalmente APIs REST e microsserviços.

---

## Exemplo completo

```go
package main

import "fmt"

// Struct
type Funcionario struct {
    Nome   string
    Salario float64
}

// Método com receiver
func (f Funcionario) ExibirDados() {

    fmt.Printf("Funcionário: %s\n", f.Nome)
    fmt.Printf("Salário: %.2f\n", f.Salario)
}

// Método com ponteiro
func (f *Funcionario) AumentarSalario(valor float64) {

    f.Salario += valor
}

func main() {

    funcionario := Funcionario{
        Nome:   "Carlos",
        Salario: 5000,
    }

    funcionario.ExibirDados()

    funcionario.AumentarSalario(1000)

    fmt.Println("Novo salário:", funcionario.Salario)
}
```

---

## Próximos passos

Agora que aprendemos a criar estruturas personalizadas e métodos em Go, o próximo passo é entender como funciona o tratamento de erros na linguagem.

➡️ [Tratamento de Erros](06-erros.md)

---

## Resumo

Nesta página aprendemos:

- O que são Structs
- Como criar Structs
- Métodos
- Receivers
- Ponteiros
- Structs aninhadas
- Structs anônimas
- Manipulação de dados complexos

!!! note "Resumo Final"
    Structs e Métodos são fundamentais em Go para modelar entidades e organizar comportamentos de forma limpa, eficiente e escalável.
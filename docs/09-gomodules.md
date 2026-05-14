# Go Modules

O sistema de gerenciamento de dependências do Go é chamado de **Go Modules**.

Ele permite organizar projetos, instalar bibliotecas externas e controlar versões de dependências de forma simples e eficiente.

Antes do Go Modules, o gerenciamento de pacotes em Go era muito mais complexo e dependia do `GOPATH`.

Atualmente, Go Modules é o padrão oficial da linguagem.

---

## O que é um Go Module?

Um Go Module é um projeto Go com gerenciamento próprio de dependências.

Todo módulo possui um arquivo chamado:

```text
go.mod
```

Esse arquivo contém:

- Nome do projeto
- Versão do Go
- Dependências instaladas

---

## Criando um projeto com Go Modules

### Passo 1 — Criar a pasta do projeto

```bash
mkdir api-go
```

---

### Passo 2 — Entrar na pasta

```bash
cd api-go
```

---

### Passo 3 — Inicializar o módulo

```bash
go mod init api-go
```

Resultado:

```text
go: creating new go.mod: module api-go
```

---

## Estrutura do projeto

Após executar o comando, o projeto ficará assim:

```text
api-go/
├── go.mod
└── main.go
```

---

## Entendendo o arquivo `go.mod`

### Exemplo

```go
module api-go

go 1.24
```

---

## Explicando cada linha

| Linha | Função |
|---|---|
| `module api-go` | Nome do módulo |
| `go 1.24` | Versão do Go utilizada |

---

## Criando o primeiro arquivo

### Exemplo de `main.go`

```go
package main

import "fmt"

func main() {

    fmt.Println("Projeto com Go Modules")
}
```

---

# Instalando dependências

Go Modules permite instalar bibliotecas externas facilmente.

---

## Exemplo com biblioteca externa

Vamos instalar o framework HTTP `Gin`.

### Comando

```bash
go get github.com/gin-gonic/gin
```

---

## Resultado no `go.mod`

```go
module api-go

go 1.24

require github.com/gin-gonic/gin v1.10.0
```

---

## Utilizando a dependência

### Exemplo

```go
package main

import "github.com/gin-gonic/gin"

func main() {

    router := gin.Default()

    router.GET("/", func(c *gin.Context) {

        c.JSON(200, gin.H{
            "message": "API funcionando",
        })
    })

    router.Run()
}
```

---

## Arquivo `go.sum`

Além do `go.mod`, Go cria automaticamente:

```text
go.sum
```

Esse arquivo armazena hashes de segurança das dependências instaladas.

---

## Diferença entre `go.mod` e `go.sum`

| Arquivo | Função |
|---|---|
| `go.mod` | Lista dependências |
| `go.sum` | Valida integridade |

!!! note "Nota Importante"
    Nunca remova o arquivo `go.sum`. Ele é essencial para segurança e consistência do projeto.

---

# Principais comandos do Go Modules

## `go mod init`

Inicializa um módulo.

```bash
go mod init nome-projeto
```

---

## `go get`

Instala dependências.

```bash
go get github.com/gin-gonic/gin
```

---

## `go mod tidy`

Remove dependências não utilizadas e organiza o projeto.

```bash
go mod tidy
```

!!! tip "Dica de Ouro"
    Execute `go mod tidy` frequentemente para manter o projeto limpo e organizado.

---

## `go mod download`

Baixa dependências manualmente.

```bash
go mod download
```

---

## `go list -m all`

Lista todos os módulos instalados.

```bash
go list -m all
```

---

# Versionamento de dependências

Go Modules suporta versionamento semântico.

### Exemplo

```text
v1.2.0
```

---

## Estrutura do versionamento

| Parte | Significado |
|---|---|
| `v1` | Versão principal |
| `2` | Novas funcionalidades |
| `0` | Correções |

---

## Atualizando dependências

### Exemplo

```bash
go get -u
```

---

## Atualizando dependência específica

```bash
go get github.com/gin-gonic/gin@latest
```

---

# Dependências diretas e indiretas

Go diferencia dependências utilizadas diretamente e dependências internas de bibliotecas.

### Exemplo

```go
require (
    github.com/gin-gonic/gin v1.10.0
)

require (
    github.com/go-playground/validator/v10 v10.20.0 // indirect
)
```

---

## Dependência indireta

Dependências indiretas são bibliotecas utilizadas por outras bibliotecas.

---

# Trabalhando com múltiplos arquivos

Em projetos maiores, normalmente utilizamos múltiplos pacotes.

---

## Exemplo de estrutura profissional

```text
api-go/
├── go.mod
├── go.sum
├── main.go
├── handlers/
├── services/
├── repositories/
└── models/
```

---

# Importando pacotes internos

### Estrutura

```text
api-go/
├── go.mod
├── main.go
└── utils/
    └── mensagem.go
```

---

## Arquivo `mensagem.go`

```go
package utils

func Mensagem() string {

    return "Olá do pacote utils"
}
```

---

## Arquivo `main.go`

```go
package main

import (
    "fmt"
    "api-go/utils"
)

func main() {

    fmt.Println(utils.Mensagem())
}
```

---

# Proxy de módulos do Go

O Go utiliza servidores proxy para acelerar downloads e melhorar segurança.

---

## Proxy padrão

```text
https://proxy.golang.org
```

---

# Variável `GOPROXY`

Podemos configurar proxies personalizados.

### Exemplo

```bash
export GOPROXY=https://proxy.golang.org
```

---

# Vendoring

Go permite armazenar dependências localmente no projeto.

---

## Criando pasta vendor

```bash
go mod vendor
```

Resultado:

```text
vendor/
```

---

## Quando utilizar Vendor?

| Cenário | Recomendado |
|---|---|
| Ambientes offline | ✅ |
| Empresas com políticas restritas | ✅ |
| Projetos simples | ❌ |

---

# Boas práticas com Go Modules

| Boa prática | Motivo |
|---|---|
| Utilizar `go mod tidy` | Projeto limpo |
| Versionar `go.mod` e `go.sum` | Reprodutibilidade |
| Evitar dependências desnecessárias | Melhor performance |
| Organizar pacotes corretamente | Melhor arquitetura |

!!! warning "Cuidado"
    Instalar muitas dependências externas pode aumentar complexidade, vulnerabilidades e tamanho do projeto.

---

# Exemplo completo

## Inicialização

```bash
go mod init api-go
```

---

## Instalação de dependência

```bash
go get github.com/gin-gonic/gin
```

---

## Código principal

```go
package main

import "fmt"

func main() {

    fmt.Println("Projeto configurado com Go Modules")
}
```

---

## Estrutura final

```text
api-go/
├── go.mod
├── go.sum
└── main.go
```

---

## Próximos passos

Agora que aprendemos a gerenciar dependências em Go, o próximo passo é estudar testes automatizados.

➡️ [Testes Automatizados](10-testes.md)

---

## Resumo

Nesta página aprendemos:

- O que são Go Modules
- Arquivo `go.mod`
- Arquivo `go.sum`
- Instalação de dependências
- Versionamento
- Estrutura de projetos
- Importação de pacotes
- Boas práticas

!!! note "Resumo Final"
    Go Modules revolucionou o gerenciamento de dependências na linguagem Go, tornando projetos mais organizados, seguros e profissionais.
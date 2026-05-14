# Introdução e Instalação

A linguagem Go (ou Golang) foi criada pela Google com o objetivo de oferecer uma linguagem simples, rápida, segura e altamente eficiente para aplicações modernas, especialmente sistemas distribuídos, APIs, microsserviços e aplicações cloud-native.

Go tornou-se extremamente popular no ecossistema DevOps e Cloud Computing devido à sua excelente performance, compilação rápida e suporte nativo à concorrência.

---

## O que é a linguagem Go?

Go é uma linguagem de programação compilada, fortemente tipada e com sintaxe simples. Foi projetada para resolver problemas comuns encontrados em linguagens mais complexas, mantendo alta performance e facilidade de manutenção.

### Principais características do Go

| Característica | Descrição |
|---|---|
| Simplicidade | Sintaxe limpa e fácil de aprender |
| Performance | Compilação rápida e execução eficiente |
| Concorrência Nativa | Suporte integrado com Goroutines e Channels |
| Multiplataforma | Funciona em Windows, Linux e macOS |
| Garbage Collector | Gerenciamento automático de memória |
| Forte Integração com DevOps | Muito utilizada em Docker, Kubernetes e Terraform |

!!! tip "Dica de Ouro"
    Go é amplamente utilizada em ferramentas modernas de infraestrutura cloud. Aprender Go é um diferencial importante para áreas de DevOps, Backend e Sistemas Distribuídos.

---

## Por que utilizar Go?

Go é utilizada por grandes empresas e projetos open-source devido à sua eficiência e escalabilidade.

### Tecnologias famosas desenvolvidas com Go

| Projeto | Objetivo |
|---|---|
| Docker | Plataforma de containers |
| Kubernetes | Orquestração de containers |
| Terraform | Infraestrutura como código |
| Prometheus | Monitoramento e métricas |
| Grafana Loki | Sistema de logs |

!!! note "Nota Importante"
    Go foi projetada para facilitar a manutenção de sistemas grandes e equipes com múltiplos desenvolvedores.

---

## Instalação do Go

O primeiro passo é instalar o compilador oficial da linguagem.

### Download oficial

Faça o download através do site oficial:

- https://go.dev/dl/

---

## Instalação no Windows

1. Acesse o instalador oficial.
2. Baixe a versão `.msi`.
3. Execute o instalador.
4. Finalize normalmente utilizando as opções padrão.

### Verificando a instalação

Abra o terminal (`CMD` ou `PowerShell`) e execute:

```bash
go version
```

Saída esperada:

```bash
go version go1.25 windows/amd64
```

!!! warning "Cuidado"
    Caso o comando `go version` não funcione, reinicie o terminal ou verifique se o Go foi adicionado corretamente ao PATH do sistema.

---

## Instalação no Linux

### Ubuntu / Debian

```bash
sudo apt update
sudo apt install golang-go -y
```

### Verificando a instalação

```bash
go version
```

---

## Instalação no macOS

Utilizando o Homebrew:

```bash
brew install go
```

### Verificando a instalação

```bash
go version
```

---

## Estrutura básica do ambiente Go

Após instalar o Go, alguns comandos tornam-se disponíveis no terminal.

| Comando | Função |
|---|---|
| `go version` | Mostra a versão instalada |
| `go run` | Executa um programa Go |
| `go build` | Compila o projeto |
| `go mod init` | Inicializa um módulo Go |
| `go test` | Executa testes automatizados |

---

## Criando o primeiro programa em Go

Crie um ficheiro chamado `main.go`.

### Exemplo inicial

```go
package main

import "fmt"

// Função principal do programa
func main() {

    // Exibe uma mensagem no terminal
    fmt.Println("Olá, Go!")
}
```

---

## Executando o programa

No terminal, execute:

```bash
go run main.go
```

Resultado esperado:

```bash
Olá, Go!
```

!!! note "Nota Importante"
    Todo programa executável em Go precisa obrigatoriamente do pacote `main` e da função `main()`.

---

## Entendendo a estrutura do código

### Componentes principais

| Elemento | Função |
|---|---|
| `package main` | Define o pacote principal |
| `import` | Importa bibliotecas |
| `func main()` | Função inicial do programa |
| `fmt.Println()` | Exibe texto no terminal |

---

## Como funciona a compilação em Go

Uma das maiores vantagens do Go é sua velocidade de compilação.

### Compilando um executável

```bash
go build main.go
```

Após executar o comando:

- Windows → gera `main.exe`
- Linux/macOS → gera `main`

---

## Organização recomendada de projetos

Uma estrutura simples e profissional normalmente segue este padrão:

```text
meu-projeto/
├── go.mod
├── main.go
├── internal/
├── pkg/
└── README.md
```

!!! tip "Dica de Ouro"
    Organizar corretamente o projeto desde o início facilita manutenção, testes e escalabilidade da aplicação.

---

## Próximos passos

Agora que o ambiente está configurado, o próximo passo é aprender a sintaxe básica da linguagem Go:

➡️ [Sintaxe Básica e Variáveis](02-sintaxe.md)

---

## Resumo

Nesta página aprendemos:

- O que é a linguagem Go
- Principais vantagens da linguagem
- Como instalar o Go
- Como verificar a instalação
- Como criar o primeiro programa
- Como executar e compilar aplicações Go
- Estrutura inicial de um projeto

!!! note "Resumo Final"
    Go é uma linguagem moderna, rápida e extremamente utilizada em ambientes cloud e DevOps. Dominar sua base é essencial para evoluir em desenvolvimento backend e infraestrutura moderna.
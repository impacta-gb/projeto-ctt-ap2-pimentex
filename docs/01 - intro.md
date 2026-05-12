# Introdução e Instalação

A linguagem Go (ou Golang) é uma linguagem de programação de código aberto desenvolvida pela Google. Ela foi criada para resolver problemas de escala em servidores, sendo conhecida pela sua simplicidade, altíssima performance e facilidade de aprendizado.

!!! tip "Dica de Instalação"
    Para instalar o Go na sua máquina, acesse o site oficial [go.dev](https://go.dev/) e baixe o instalador correspondente ao seu sistema operacional. Após a instalação, abra o terminal e digite `go version` para confirmar que deu tudo certo!

## O clássico "Hello World"

O Go foi desenhado para ser limpo e direto. Todo programa executável em Go precisa obrigatoriamente estar dentro de um pacote chamado `main`.

Veja o exemplo abaixo com Syntax Highlighting:

```go
package main

// O pacote 'fmt' (format) é usado para formatar textos e imprimir na tela
import "fmt"

func main() {
    fmt.Println("Olá, Mundo! Bem-vindos à documentação do Projeto CTT-AP2.")
}
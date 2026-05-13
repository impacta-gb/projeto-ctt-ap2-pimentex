# 10 - Testes Automatizados

Go possui suporte nativo para testes através do pacote `testing`.

!!! success "Comando de Teste"
    Rode `go test` no terminal para executar todas as validações do seu projeto.

```go
func TestSoma(t *testing.T) {
    if Soma(2,2) != 4 {
        t.Error("Falha no teste de soma")
    }
}
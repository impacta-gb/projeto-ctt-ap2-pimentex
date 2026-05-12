# 06 - Tratamento de Erros

Em Go, erros são valores retornados pelas funções, e não exceções que interrompem o fluxo inesperadamente.

!!! danger "Verificação Obrigatória"
    Sempre verifique se `err != nil` para garantir a resiliência do código.

```go
func validar(email string) error {
    if email == "" {
        return errors.New("email vazio")
    }
    return nil
}
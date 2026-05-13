# 08 - Channels

Canais são as tubulações que permitem que Goroutines se comuniquem e sincronizem dados de forma segura.

```go
ch := make(chan string)
go func() { ch <- "Dados enviados" }()
msg := <-ch
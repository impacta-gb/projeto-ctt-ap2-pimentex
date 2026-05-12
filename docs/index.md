# Projeto CTT-AP2

Bem-vindo à documentação oficial da linguagem Go, desenvolvida pelo grupo **Impacta-GB (Pimentex)**. Este site foi construído utilizando o gerador estático **Zensical** e automatizado via **GitHub Actions**.

!!! tip "Objetivo do Projeto"
    Criar uma base de conhecimento técnica e robusta sobre Go, aplicando fluxos de trabalho colaborativos (Feature Branches e Pull Requests) e integração contínua (CI/CD).

---

## 📚 Módulos de Aprendizado

Utilize a tabela abaixo para navegar pelos tópicos da linguagem. Cada seção foi revisada e validada através de nosso pipeline de CI/CD.

| Ordem | Tópico da Documentação | Descrição Breve |
| :---: | :--- | :--- |
| 1 | [**Introdução e Instalação**](01 - intro.md) | Primeiros passos e configuração do ambiente Go. |
| 2 | [**Sintaxe Básica e Variáveis**](02 - sintaxe.md) | Tipagem, declarações e estrutura de código. |
| 3 | [**Estruturas de Controle**](03 - ifForswitch.md) | Controle de fluxo com If, For e Switch. |
| 4 | [**Arrays, Slices e Maps**](04 - colecoes.md) | Como lidar com coleções de dados no Go. |
| 5 | [**Structs e Métodos**](05 - structs.md) | Orientação a objetos e estruturas customizadas. |
| 6 | [**Tratamento de Erros**](06 - errors.md) | Boas práticas para lidar com exceções. |
| 7 | [**Concorrência: Goroutines**](07 - goroutines.md) | O poder do processamento paralelo. |
| 8 | [**Concorrência: Channels**](08 - channels.md) | Comunicação entre processos concorrentes. |
| 9 | [**Go Modules**](09 - gomodules.md) | Gerenciamento de pacotes e dependências. |
| 10 | [**Testes Automatizados**](10 - testes.md) | Garantindo a qualidade do código Go. |

---

## 🛠️ Sobre a Infraestrutura

Este projeto utiliza uma arquitetura de **CI/CD moderna**:
- **Matrix Strategy:** Validação do build em Python 3.10 e 3.11.
- **Carga Otimizada:** Uso de cache para dependências `pip`.
- **Deploy Seguro:** Separação entre os estágios de *Build* e *Deploy*.

---
*Gerado para a disciplina de Cloud & DevOps - Impacta 2026.*
# Documentação da Linguagem Go com Zensical

##  Sobre o Projeto

Este projeto foi desenvolvido como atividade prática da disciplina de CTT AP2 com o objetivo de criar uma documentação da linguagem Go utilizando a ferramenta Zensical.

Além da criação das páginas de documentação, o projeto teve como foco principal a aplicação de boas práticas de desenvolvimento colaborativo e automação de CI/CD utilizando GitHub Actions e GitHub Pages.

---

##  Objetivos do Projeto

- Criar um site de documentação estática sobre a linguagem Go
- Aplicar fluxo colaborativo utilizando Git e GitHub
- Utilizar Feature Branches, Pull Requests e Code Reviews
- Implementar um pipeline completo de CI/CD
- Automatizar o deploy da documentação no GitHub Pages
- Garantir validação do projeto em múltiplas versões do Python

---

##  Tecnologias Utilizadas

- Go (conteúdo da documentação)
- Python
- Zensical
- Git
- GitHub
- GitHub Actions
- GitHub Pages
- Markdown

---

##  Site Publicado

> ```text
https://impacta-gb.github.io/projeto-ctt-ap2-pimentex/
```

---

##  Estrutura do Projeto

```text
.
├── .github/
│   └── workflows/
│       └── docs.yml
├── docs/
│   ├── index.md
│   ├── introducao.md
│   ├── sintaxe.md
│   ├── goroutines.md
│   └── ...
├── zensical.yml
└── README.md
```

---

##  Fluxo de Trabalho Colaborativo

O projeto seguiu um fluxo colaborativo baseado em boas práticas utilizadas em ambientes profissionais.

###  Feature Branches

Cada funcionalidade ou página da documentação foi desenvolvida em uma branch separada.

Exemplos:

```text
feat/introducao-go
feat/goroutines
fix/workflow-cache
```

---

###  Pull Requests e Code Review

Todas as alterações foram realizadas através de Pull Requests (PRs).

O processo adotado foi:

1. Criação da feature branch
2. Desenvolvimento da funcionalidade
3. Push para o repositório remoto
4. Abertura de Pull Request
5. Revisão por outro integrante do grupo
6. Aprovação do PR
7. Merge na branch `main`

---

###  Proteção da Branch Main

A branch `main` foi protegida utilizando Branch Protection Rules no GitHub.

As seguintes restrições foram aplicadas:

- Bloqueio de pushes diretos
- Obrigatoriedade de Pull Requests
- Necessidade de aprovação para merge
- Revisão obrigatória por pelo menos um integrante

---

##  Pipeline CI/CD

O projeto utiliza GitHub Actions para automação dos processos de integração contínua e deploy contínuo.

O workflow foi configurado em:

```text
.github/workflows/docs.yml
```

---

##  Gatilhos do Workflow

O pipeline é executado automaticamente nos seguintes eventos:

### Pull Request

Executa validações antes do merge na branch principal.

### Push na Main

Executa build e deploy automático após integração aprovada.

### Schedule (Cron)

O workflow também executa semanalmente através de um agendamento automático. Realizado aos domingos a meia-noite.

```yaml
cron: "0 0 * * 0"
```

---

##  Estratégia Matrix

O job de validação utiliza Matrix Strategy para testar múltiplas versões do Python.

Versões utilizadas:

- Python 3.10
- Python 3.11

Isso garante compatibilidade do projeto em diferentes ambientes.

---

##  Cache de Dependências

Foi implementado cache utilizando `actions/cache` para otimizar o tempo de execução do pipeline e evitar reinstalações desnecessárias das dependências Python.

---

##  Separação de Jobs e Artefatos

O pipeline foi dividido em dois jobs principais:

### build_site

Responsável por:

- Instalar dependências
- Gerar o site estático
- Validar a documentação
- Gerar artefatos

### deploy_site

Responsável por:

- Baixar os artefatos gerados
- Publicar automaticamente no GitHub Pages

A comunicação entre os jobs foi realizada utilizando upload e download de artefatos.

---

##  Segurança no Deploy

O deploy foi protegido utilizando condicionais com `if`.

O job de deploy não é executado durante Pull Requests.

Exemplo:

```yaml
if: github.event_name != 'pull_request'
```

Isso garante que apenas alterações aprovadas sejam publicadas.

---

##  Como Executar o Projeto Localmente

### Instalar dependências

```bash
pip install zensical
```

---

### Executar servidor local

```bash
python -m zensical serve
```

O projeto ficará disponível em:

```text
http://localhost:8000
```

---

##  Conteúdos da Documentação

A documentação aborda os seguintes temas da linguagem Go:

- Introdução e Instalação
- Sintaxe Básica e Variáveis
- Estruturas de Controle
- Arrays, Slices e Maps
- Structs e Métodos
- Tratamento de Erros
- Goroutines
- Channels
- Go Modules
- Testes Automatizados

---

##  Integrantes

- Cauê Fernandes Santos
- Pedro Henrique Fusco
- Pedro Luiz Martins de Oliveira

---

##  Resultados Obtidos

- Fluxo colaborativo implementado com sucesso
- CI/CD automatizado
- Deploy automático funcional
- Branch principal protegida
- Documentação validada automaticamente
- Integração com GitHub Pages concluída

---

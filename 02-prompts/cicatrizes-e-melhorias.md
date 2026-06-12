# Cicatrizes e Melhorias

## 📌 Objetivo

Este arquivo registra alguns ajustes feitos durante o uso do NotebookLM no estudo sobre **Arquitetura de APIs para Pagamentos Digitais e Mobilidade**.

A intenção é mostrar como os prompts foram melhorados ao longo do processo para gerar respostas mais úteis, menos genéricas e mais conectadas ao problema estudado.

## ⚠️ Cicatriz 1 - Perguntas muito amplas geravam respostas genéricas

### Prompt inicial

```text
Explique o que são APIs.
```

### Problema encontrado

A resposta ficava correta, mas superficial. Ela explicava o conceito de API de forma ampla, sem conectar o tema ao contexto de pagamentos digitais, mobilidade ou arquitetura de sistemas.

### Prompt melhorado

```text
Com base exclusivamente nas fontes adicionadas, explique em linguagem simples o que é uma arquitetura de APIs aplicada a sistemas de pagamentos digitais e mobilidade.
```

### Melhoria percebida

A resposta passou a trazer conceitos mais alinhados ao projeto, como API-First, microsserviços, API Gateway, eventos, segurança e idempotência.

## ⚠️ Cicatriz 2 - O estudo estava ficando teórico demais

### Prompt inicial

```text
Explique arquitetura de APIs.
```

### Problema encontrado

A explicação ajudava no entendimento conceitual, mas ainda faltava uma aplicação prática para visualizar o funcionamento da arquitetura em um cenário realista.

### Prompt melhorado

```text
Crie um exemplo prático de arquitetura para um sistema que registra uma passagem em pedágio ou estacionamento, valida o cliente, calcula o valor, registra a transação e gera uma cobrança.
```

### Melhoria percebida

A resposta conectou os conceitos estudados a um fluxo mais concreto, envolvendo captura de evento, validação, desduplicação, cálculo, registro da transação e cobrança.

## ⚠️ Cicatriz 3 - O fluxo ideal não mostrava os riscos

### Prompt inicial

```text
Explique como funciona uma API de pagamento.
```

### Problema encontrado

A resposta focava no funcionamento esperado do sistema, mas não explorava bem os riscos técnicos envolvidos em APIs críticas.

### Prompt melhorado

```text
Quais são os principais riscos técnicos em uma API de pagamentos e mobilidade? Explique também quais boas práticas podem reduzir esses riscos.
```

### Melhoria percebida

O NotebookLM passou a destacar riscos como cobrança duplicada, falhas de autenticação, exposição de dados sensíveis, inconsistência de dados e indisponibilidade. Também trouxe boas práticas como idempotência, API Gateway, criptografia, observabilidade e versionamento.

## ✅ Síntese das melhorias

| Cicatriz               | Ajuste feito                         | Resultado                          |
| ---------------------- | ------------------------------------ | ---------------------------------- |
| Perguntas amplas       | Adição de contexto e recorte do tema | Respostas mais direcionadas        |
| Conteúdo muito teórico | Solicitação de exemplo prático       | Melhor conexão com cenário real    |
| Falta de visão crítica | Inclusão de riscos e boas práticas   | Análise mais madura da arquitetura |

## 💡 Aprendizado principal

O principal aprendizado foi que bons prompts não precisam ser complexos, mas precisam ser bem direcionados.

Quando a pergunta trouxe contexto, objetivo e um cenário de aplicação, as respostas ficaram mais úteis para transformar o estudo em documentação técnica.

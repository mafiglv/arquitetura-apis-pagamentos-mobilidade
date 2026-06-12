# Prompts Testados

## 📌 Objetivo

Este arquivo registra os principais prompts utilizados no NotebookLM durante o estudo sobre **Arquitetura de APIs para Pagamentos Digitais e Mobilidade**.

A ideia foi usar os prompts como ferramenta de investigação técnica: primeiro para entender o domínio, depois para organizar os conceitos, aplicar em um cenário prático e mapear riscos.

## 🧠 Estratégia

Os prompts foram organizados em uma sequência simples:

1. entender o conceito geral;
2. estruturar uma trilha de estudo;
3. consolidar os principais pontos;
4. criar um glossário técnico;
5. aplicar o conteúdo em um fluxo realista;
6. mapear riscos e boas práticas.

## 🔎 Prompt 1 — Entendimento inicial

```text
Com base exclusivamente nas fontes adicionadas, explique em linguagem simples o que é uma arquitetura de APIs aplicada a sistemas de pagamentos digitais e mobilidade.
```

**Objetivo:**
Criar uma visão inicial do tema sem começar por uma explicação excessivamente técnica.

**Resultado:**
O NotebookLM apresentou a arquitetura de APIs como uma estrutura que conecta sistemas, canais digitais e serviços de pagamento/mobilidade. A resposta trouxe os primeiros conceitos-chave: API-First, microsserviços, API Gateway, eventos, segurança e idempotência.

**Aprendizado:**
Esse prompt ajudou a definir o ponto de partida do estudo e mostrou quais conceitos precisariam ser aprofundados depois.

## 🗺️ Prompt 2 — Roteiro de estudo

```text
Organize o conteúdo das fontes em um roteiro de estudo com os principais tópicos que eu preciso aprender para entender arquitetura de APIs em sistemas de pagamentos digitais e mobilidade.
```

**Objetivo:**
Transformar o conteúdo das fontes em uma trilha lógica de aprendizagem.

**Resultado:**
O NotebookLM organizou o estudo em fases: fundamentos de APIs, microsserviços, arquitetura orientada a eventos, sistemas de pagamento, segurança, resiliência e observabilidade.

**Aprendizado:**
Esse prompt foi importante para definir a estrutura do miniguia e evitar que o conteúdo ficasse solto.

## 🧾 Prompt 3 — Resumo estruturado

```text
Crie um resumo estruturado do tema, separando por tópicos: conceito geral, principais componentes, funcionamento do fluxo, riscos, boas práticas e exemplos práticos.
```

**Objetivo:**
Consolidar o estudo em uma visão mais organizada e reutilizável.

**Resultado:**
A resposta separou o tema em blocos claros: conceito geral, componentes, fluxo, riscos, boas práticas e exemplos.

**Aprendizado:**
O resumo ajudou a transformar as respostas do NotebookLM em conteúdo base para o arquivo `resumo-estruturado.md`.

## 📚 Prompt 4 — Glossário técnico

```text
Crie um glossário com os principais conceitos técnicos das fontes, explicando cada termo de forma simples e objetiva.
```

**Objetivo:**
Mapear os principais termos técnicos do estudo.

**Resultado:**
Foram listados conceitos como API-First, REST, microsserviços, arquitetura orientada a eventos, API Gateway, endpoint, ACID, idempotência, tokenização, escalabilidade, desacoplamento e payload.

**Aprendizado:**
O glossário ajudou a padronizar a linguagem do projeto e serviu como material de consulta rápida.

## 🏗️ Prompt 5 — Aplicação prática

```text
Crie um exemplo prático de arquitetura para um sistema que registra uma passagem em pedágio ou estacionamento, valida o cliente, calcula o valor, registra a transação e gera uma cobrança.
```

**Objetivo:**
Aplicar os conceitos em um cenário próximo de um sistema real de mobilidade e pagamento.

**Resultado:**
O NotebookLM sugeriu uma arquitetura com captura de evento, API Gateway, validação, desduplicação, identificação do cliente, cálculo do valor, registro da transação, fila de cobrança, gateway de pagamento e persistência em banco/ledger.

**Aprendizado:**
Esse foi o prompt mais relevante para conectar teoria e prática. Ele serviu de base para os arquivos da pasta `04-arquitetura`.

## ⚠️ Prompt 6 — Riscos e boas práticas

```text
Quais são os principais riscos técnicos em uma API de pagamentos e mobilidade? Explique também quais boas práticas podem reduzir esses riscos.
```

**Objetivo:**
Avaliar o tema pelo ponto de vista de falhas, riscos e mitigação.

**Resultado:**
A resposta destacou riscos como cobrança duplicada, falhas de autenticação e autorização, exposição de dados sensíveis, inconsistência de dados, latência, indisponibilidade e dificuldade de depuração em sistemas distribuídos.

Também foram citadas boas práticas como idempotência, API Gateway, tokenização, criptografia, observabilidade, rastreamento distribuído, versionamento e padrões de resiliência.

**Aprendizado:**
Esse prompt trouxe uma visão mais madura do estudo, porque deixou de focar apenas no “fluxo ideal” e passou a considerar o que pode dar errado em produção.

## 📊 Síntese

| Prompt | Foco              | Entrega gerada                      |
| ------ | ----------------- | ----------------------------------- |
| 1      | Conceito geral    | Base inicial do tema                |
| 2      | Roteiro de estudo | Estrutura da trilha de aprendizagem |
| 3      | Resumo            | Conteúdo para o miniguia            |
| 4      | Glossário         | Padronização dos termos técnicos    |
| 5      | Exemplo prático   | Base da arquitetura conceitual      |
| 6      | Riscos            | Mapa de riscos e boas práticas      |

## ✅ Conclusão

Os prompts foram utilizados de forma progressiva para transformar as fontes em um estudo organizado.

O principal aprendizado foi que prompts mais específicos geram respostas melhores. Quando a pergunta trouxe contexto, objetivo e recorte do problema, o NotebookLM entregou respostas mais úteis para análise técnica e documentação.

Neste projeto, a IA foi usada como apoio ao raciocínio, não como substituta da curadoria. O resultado final dependeu da combinação entre boas fontes, perguntas bem formuladas e organização crítica das respostas.

# Perguntas de Revisão

## 📌 Objetivo

Este arquivo reúne perguntas de revisão sobre os principais conceitos estudados no caderno temático: **API-First, APIs REST, microsserviços, arquitetura orientada a eventos, sistemas de pagamento, API Gateway, idempotência e versionamento de APIs**.

A proposta é usar as perguntas como material de fixação e revisão rápida.

## 1. Shopify x Basecamp: diferença estratégica de arquitetura

**Pergunta:**
De acordo com a análise de Guilherme Favaron, qual é a principal diferença estratégica entre a abordagem da Shopify e a do Basecamp em relação à arquitetura?

**A.** A Shopify prioriza um ecossistema aberto via APIs para permitir extensibilidade por terceiros, enquanto o Basecamp foca em um monólito coeso para manter a simplicidade e eficiência da equipe.
**B.** Ambas as empresas adotam a estratégia API-first como dogma absoluto para garantir a sobrevivência no mercado tecnológico moderno.
**C.** A Shopify foca exclusivamente em performance de hardware, enquanto o Basecamp foca em integração com múltiplos canais de IoT.
**D.** O Basecamp utiliza uma arquitetura de microsserviços distribuídos para garantir lucro, enquanto a Shopify mantém um monólito para processar bilhões de dólares.

**Resposta correta:** A

**Comentário:**
A diferença está na estratégia de negócio e arquitetura. A Shopify se beneficia de um ecossistema extensível por APIs, enquanto o Basecamp prioriza simplicidade operacional com um monólito mais coeso.

## 2. Quando API-First pode ser over-engineering

**Pergunta:**
Em quais situações a arquitetura API-first é considerada over-engineering?

**A.** Em sistemas que precisam entregar experiências consistentes em múltiplos canais como web, mobile e IoT.
**B.** Quando o modelo de negócio depende obrigatoriamente de integrações com ecossistemas de parceiros externos.
**C.** Em produtos em estágio inicial buscando product-market fit, onde a agilidade para pivotar é mais crítica que a disciplina arquitetural.
**D.** Quando a empresa precisa escalar componentes de forma independente para reduzir custos de infraestrutura.

**Resposta correta:** C

**Comentário:**
Em produtos muito iniciais, criar uma arquitetura API-First completa pode ser excesso de engenharia. Nessa fase, muitas vezes a prioridade é validar o produto rapidamente.

## 3. Vantagem da arquitetura orientada a eventos

**Pergunta:**
Qual é a principal vantagem de uma arquitetura baseada em eventos em comparação ao modelo tradicional de requisição-resposta?

**A.** Permite o processamento assíncrono e o baixo acoplamento, onde os componentes podem ser escalados e evoluídos de forma independente.
**B.** O Componente A deve obrigatoriamente aguardar a resposta do Componente B para finalizar sua execução, aumentando a consistência síncrona.
**C.** O acoplamento forte entre os componentes garante que o sistema nunca perca mensagens durante o processamento.
**D.** Elimina a necessidade de bancos de dados relacionais, substituindo-os completamente por barramentos de mensagens.

**Resposta correta:** A

**Comentário:**
A arquitetura orientada a eventos favorece comunicação assíncrona, desacoplamento e escalabilidade independente entre componentes.

## 4. Definição de URIs em APIs RESTful

**Pergunta:**
No design de APIs RESTful, qual é a recomendação principal para a definição de URIs?

**A.** Espelhar exatamente a estrutura das tabelas do banco de dados relacional para facilitar o mapeamento interno.
**B.** Basear os URIs em substantivos que representam recursos, evitando o uso de verbos no caminho do identificador.
**C.** Utilizar verbos para representar as operações, como em `/get-all-customers` ou `/update-order`.
**D.** Utilizar nomes de recursos no singular em coleções para manter a simplicidade, como em `/customer` para listar todos.

**Resposta correta:** B

**Comentário:**
Em APIs RESTful, URIs devem representar recursos, normalmente usando substantivos. As ações são indicadas pelos métodos HTTP, como `GET`, `POST`, `PUT`, `PATCH` e `DELETE`.

## 5. Diferença entre PUT e PATCH

**Pergunta:**
Qual é a diferença fundamental entre os métodos HTTP PUT e PATCH?

**A.** O PUT substitui todo o recurso pela representação enviada, enquanto o PATCH aplica atualizações parciais ao recurso existente.
**B.** O PUT só funciona com formato XML e o PATCH só aceita formato JSON.
**C.** O PUT é utilizado para criar recursos e o PATCH para deletá-los permanentemente.
**D.** O PATCH é obrigatoriamente idempotente, enquanto o PUT pode resultar em efeitos colaterais diferentes a cada chamada.

**Resposta correta:** A

**Comentário:**
O `PUT` normalmente substitui o recurso completo. O `PATCH` é usado quando a intenção é atualizar apenas parte do recurso.

## 6. Conceito de HATEOAS

**Pergunta:**
O que caracteriza o conceito de HATEOAS em uma API RESTful?

**A.** A obrigatoriedade de utilizar criptografia de ponta a ponta em todos os endpoints de busca.
**B.** A inclusão de links de hipermídia na resposta que permitem ao cliente navegar pelos recursos relacionados sem conhecimento prévio dos URIs.
**C.** O uso de múltiplos bancos de dados NoSQL para garantir a alta disponibilidade dos metadados da API.
**D.** A prática de versionar a API exclusivamente através da string de consulta.

**Resposta correta:** B

**Comentário:**
HATEOAS permite que a API indique ao cliente quais ações ou navegações são possíveis a partir do estado atual do recurso.

## 7. Idempotência em sistemas de pagamento

**Pergunta:**
Por que a idempotência é considerada um requisito não negociável em sistemas de pagamento?

**A.** Porque permite que o sistema utilize bancos de dados sem garantias ACID para reduzir custos operacionais.
**B.** Para evitar que o desenvolvedor precise documentar os endpoints da API de pagamento.
**C.** Para garantir que retentativas de uma mesma transação, causadas por timeouts ou falhas de rede, não resultem em cobranças duplicadas ao cliente.
**D.** Para aumentar a latência do sistema, permitindo que o banco de dados processe transações de forma sequencial.

**Resposta correta:** C

**Comentário:**
Em pagamentos, uma requisição pode ser reenviada por falha de rede ou timeout. A idempotência garante que essa repetição não gere uma nova cobrança indevida.

## 8. Função do API Gateway

**Pergunta:**
No contexto de um ecossistema de APIs, qual é a função primordial do API Gateway?

**A.** Atuar como um ponto de entrada único que gerencia tarefas como autenticação, balanceamento de carga e limitação de taxa.
**B.** Servir como um fórum de discussão onde desenvolvedores externos reportam bugs e sugerem melhorias.
**C.** Armazenar os dados brutos de que as aplicações precisam para funcionar, substituindo os bancos de dados tradicionais.
**D.** Gerar automaticamente o código-fonte da aplicação front-end a partir da especificação do banco de dados.

**Resposta correta:** A

**Comentário:**
O API Gateway centraliza a entrada das requisições e pode aplicar políticas de segurança, autenticação, roteamento, rate limiting e balanceamento.

## 9. Trade-off do versionamento por header ou media type

**Pergunta:**
Ao implementar o controle de versão em uma API, qual é o principal trade-off do versionamento por cabeçalho ou tipo de mídia?

**A.** Eles podem dificultar o cache em proxies da rede, pois o URI, que geralmente é usado como chave de cache, permanece o mesmo para versões diferentes.
**B.** Eles tornam os URIs extremamente longos e difíceis de ler por humanos.
**C.** Eles são a forma mais simples de implementar e não exigem lógica adicional no servidor.
**D.** Eles impedem que a API utilize o protocolo HTTP, exigindo o uso de WebSockets.

**Resposta correta:** A

**Comentário:**
Quando a versão fica no header ou no media type, o URI continua o mesmo. Isso pode complicar estratégias de cache, já que proxies geralmente usam o URI como parte importante da chave de cache.

## ✅ Gabarito rápido

| Questão | Resposta |
| ------- | -------- |
| 1       | A        |
| 2       | C        |
| 3       | A        |
| 4       | B        |
| 5       | A        |
| 6       | B        |
| 7       | C        |
| 8       | A        |
| 9       | A        |

## 📌 Síntese

As perguntas reforçam os pontos mais importantes do estudo:

* API-First deve fazer sentido para o contexto do negócio;
* nem toda solução precisa de arquitetura complexa desde o início;
* APIs REST devem representar recursos com clareza;
* arquitetura orientada a eventos favorece desacoplamento;
* idempotência é essencial em pagamentos;
* API Gateway ajuda a centralizar segurança e controle;
* decisões de versionamento envolvem trade-offs.

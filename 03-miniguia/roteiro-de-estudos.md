# Roteiro de Estudos

## 📌 Objetivo

Este roteiro de estudos foi organizado com base nas fontes adicionadas ao NotebookLM, partindo dos conceitos fundamentais de APIs até a aplicação prática em sistemas complexos de pagamentos digitais e mobilidade.

A proposta é seguir uma trilha progressiva para compreender como APIs, microsserviços, arquitetura orientada a eventos, segurança e observabilidade se conectam em soluções modernas.

## 🧱 Fase 1: Fundamentos de Arquitetura e Design de APIs

Antes de entrar em sistemas específicos, é essencial entender como as APIs modernas são projetadas.

### API-First

Compreender que a API deve ser tratada como o produto primário, definida antes mesmo da interface de usuário para garantir consistência e compatibilidade.

### Design RESTful

Aprender as práticas recomendadas para o uso de verbos HTTP, como:

* `GET`;
* `POST`;
* `PUT`;
* `DELETE`.

Também é importante entender o uso de substantivos em URIs e a comunicação via JSON.

### Modelos de maturidade e padronização

Estudar o Modelo de Maturidade de Richardson e a importância da especificação OpenAPI para documentação e interoperabilidade.

### Versionamento e paginação

Aprender estratégias para atualizar APIs sem quebrar clientes existentes e como gerenciar grandes volumes de dados.

## 🌐 Fase 2: Estilos de Arquitetura e Ecossistemas Digitais

Nesta etapa, o foco é entender como as APIs conectam diferentes partes de um negócio e parceiros.

### Monólitos vs. Microsserviços

Entender as trocas entre simplicidade, no caso do monólito, e agilidade/escala, no caso dos microsserviços.

Também é importante compreender quando adotar modelos híbridos.

### Ecossistemas de API

Estudar como as APIs criam valor de negócio ao permitir a integração de parceiros e múltiplos canais digitais, como:

* web;
* mobile;
* IoT.

Essa integração permite que diferentes canais evoluam de forma independente.

### Componentes de infraestrutura

Aprender o papel do API Gateway como ponto único de entrada e segurança.

Também é importante compreender o papel do balanceamento de carga.

## 💳 Fase 3: Arquitetura Específica para Sistemas de Pagamento

Pagamentos exigem rigor técnico devido à necessidade de integridade de dados.

### Componentes do sistema

Entender os papéis de componentes como:

* Gateway de pagamento;
* Banco adquirente;
* Banco emissor;
* Redes de cartões.

### Fluxo transacional

Estudar as etapas de:

* Autorização;
* Captura;
* Compensação, também chamada de Clearing;
* Liquidação, também chamada de Settlement.

### Consistência e integridade

Diferenciar transações ACID, que exigem consistência absoluta, de consistência eventual.

Esse ponto é especialmente importante em saldos bancários e operações financeiras.

### Idempotência

Aprender este conceito crítico para garantir que uma transação repetida, por erro de rede ou timeout, não resulte em cobranças duplicadas.

## ⚡ Fase 4: Arquitetura Orientada a Eventos

A Arquitetura Orientada a Eventos, também chamada de EDA, é um padrão moderno para sistemas de pagamento e mobilidade altamente escaláveis.

### Conceitos de EDA

Entender a diferença entre modelos baseados em solicitação, que são síncronos, e modelos baseados em eventos, que são assíncronos.

### Componentes de eventos

Estudar os papéis de:

* produtores de eventos;
* roteadores ou barramentos de eventos, como o EventBridge;
* consumidores de eventos.

### Vantagens para mobilidade

Aprender como a EDA permite:

* processamento paralelo;
* distribuição de informações, também chamada de fan-out;
* escalabilidade independente;
* melhor resposta a picos de demanda.

## 🔐 Fase 5: Segurança, Resiliência e Operações

A fase final foca na proteção e manutenção da saúde do sistema.

### OWASP API Security Top 10

Estudar as principais vulnerabilidades em APIs, como falhas de autenticação e autorização em nível de objeto.

### Observabilidade

Compreender a importância de implementar:

* rastreamento distribuído;
* logs centralizados;
* métricas.

Esses elementos ajudam a diagnosticar falhas em sistemas complexos.

### Resiliência e falhas

Aprender padrões como:

* Circuit Breaker;
* Dead Letter Queues.

Esses padrões ajudam a isolar erros e evitar que uma falha se espalhe por todo o sistema.

### Conformidade e regulação

Entender a importância de padrões como PCI DSS para segurança de dados de cartões.

## Síntese do roteiro

| Fase   | Foco principal                  | Conceitos-chave                                                     |
| ------ | ------------------------------- | ------------------------------------------------------------------- |
| Fase 1 | Fundamentos de APIs             | API-First, REST, OpenAPI, versionamento                             |
| Fase 2 | Estilos de arquitetura          | Monólito, microsserviços, ecossistemas de API                       |
| Fase 3 | Sistemas de pagamento           | Gateway, autorização, clearing, settlement, ACID, idempotência      |
| Fase 4 | Arquitetura orientada a eventos | Eventos, produtores, consumidores, EventBridge, fan-out             |
| Fase 5 | Segurança e operação            | OWASP, observabilidade, Circuit Breaker, Dead Letter Queue, PCI DSS |

## ✅ Conclusão

O roteiro mostra que entender arquitetura de APIs em pagamentos digitais e mobilidade exige uma visão progressiva.

Primeiro, é necessário compreender os fundamentos de APIs. Depois, avaliar estilos de arquitetura, entender os requisitos de sistemas de pagamento, estudar modelos orientados a eventos e, por fim, considerar segurança, resiliência e operação.

Essa sequência ajuda a conectar teoria e prática em um cenário de sistemas distribuídos, críticos e transacionais.

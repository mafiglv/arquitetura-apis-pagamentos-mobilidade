# Glossário Técnico

## 📌 Objetivo

Este glossário reúne os principais conceitos estudados no caderno temático sobre **Arquitetura de APIs para Pagamentos Digitais e Mobilidade**.

A ideia é manter uma base rápida de consulta para revisar termos importantes de APIs, arquitetura de sistemas, segurança, pagamentos digitais e mobilidade.

## 🔌 API

API significa **Application Programming Interface**.

Na prática, é uma forma padronizada de permitir que sistemas diferentes conversem entre si.

Em um sistema de mobilidade e pagamentos, uma API pode ser usada para registrar uma passagem, consultar um cliente, calcular uma tarifa ou gerar uma cobrança.

## 🧭 API-First

API-First é uma abordagem em que a API é pensada antes da interface final do produto.

Isso significa que, antes de criar uma tela ou aplicativo, o time define como os sistemas vão trocar informações.

Essa abordagem ajuda a criar integrações mais consistentes, reutilizáveis e preparadas para diferentes canais, como aplicativo, site, parceiros e sistemas internos.

## 🌐 API REST

REST é um estilo de arquitetura muito usado para criar APIs Web.

Uma API REST organiza recursos por URLs e utiliza métodos HTTP, como:

* `GET` para buscar dados;
* `POST` para criar registros;
* `PUT` ou `PATCH` para atualizar informações;
* `DELETE` para remover dados.

Esse padrão facilita a comunicação entre aplicações.

## 📍 Endpoint

Endpoint é o endereço de uma funcionalidade específica da API.

Exemplo:

```text
POST /transacoes
```

Esse endpoint poderia ser usado para registrar uma nova transação de mobilidade.

## 🧱 Microsserviços

Microsserviços são uma forma de dividir um sistema maior em serviços menores e independentes.

Cada serviço tem uma responsabilidade específica.

Em um sistema de pagamentos e mobilidade, poderiam existir serviços separados para:

* validar cliente;
* calcular tarifa;
* registrar transação;
* processar cobrança;
* enviar notificação.

Essa separação facilita manutenção e evolução, mas também exige mais cuidado com comunicação, logs e observabilidade.

## 🚪 API Gateway

API Gateway é o ponto de entrada das requisições.

Ele funciona como uma camada intermediária entre os clientes e os serviços internos.

Pode ser responsável por:

* autenticação;
* autorização;
* roteamento;
* controle de tráfego;
* rate limiting;
* logs;
* proteção dos serviços internos.

## ⚡ Arquitetura Orientada a Eventos

Arquitetura Orientada a Eventos, ou EDA, é um modelo em que os sistemas reagem a acontecimentos.

Exemplos de eventos:

* passagem registrada;
* pagamento aprovado;
* cobrança gerada;
* cliente validado.

Esse modelo ajuda a reduzir o acoplamento entre serviços e permite processamentos assíncronos.

## 📨 Evento

Evento é o registro de algo que aconteceu no sistema.

Em vez de um serviço chamar diretamente outro serviço, ele pode publicar um evento.

Exemplo:

```text
pagamento_aprovado
```

Outros serviços podem escutar esse evento e executar ações, como enviar recibo, atualizar histórico ou liberar acesso.

## 🔁 Idempotência

Idempotência é a garantia de que uma mesma operação pode ser repetida sem gerar efeito duplicado.

Em pagamentos, isso é essencial.

Se uma requisição de cobrança for enviada duas vezes por erro de rede, o sistema precisa entender que se trata da mesma operação e evitar cobrar o cliente duas vezes.

## 🧾 Payload

Payload é o conjunto de dados enviado ou recebido em uma requisição.

Exemplo de payload para registrar uma transação:

```json
{
  "clienteId": "123",
  "placa": "ABC1D23",
  "local": "Estacionamento Centro",
  "valor": 12.50
}
```

## 🔐 Autenticação

Autenticação é o processo de verificar quem está acessando o sistema.

Exemplo: confirmar se um usuário, aplicação ou serviço possui uma identidade válida.

Em APIs, isso pode ser feito com tokens, chaves de API ou outros mecanismos de segurança.

## 🛂 Autorização

Autorização define o que uma identidade autenticada pode fazer.

Exemplo: um sistema pode estar autenticado, mas não ter permissão para consultar dados financeiros ou criar cobranças.

## 🪙 Tokenização

Tokenização é o processo de substituir um dado sensível por um token.

Em pagamentos, isso pode ser usado para evitar que dados de cartão fiquem expostos diretamente nos sistemas.

Em vez de armazenar o número real do cartão, o sistema trabalha com um identificador seguro.

## 🔒 Criptografia

Criptografia é uma técnica usada para proteger dados.

Ela pode ser aplicada:

* em trânsito, quando os dados estão sendo enviados entre sistemas;
* em repouso, quando os dados estão armazenados.

Em sistemas de pagamento, criptografia é fundamental para proteger informações sensíveis.

## 💳 Gateway de Pagamento

Gateway de pagamento é o componente responsável por intermediar a comunicação entre o sistema da empresa e as instituições financeiras.

Ele ajuda a processar pagamentos, autorizações, confirmações e retornos das transações.

## 🏦 Banco Emissor

Banco emissor é a instituição que emitiu o cartão ou meio de pagamento do cliente.

Ele pode aprovar ou negar uma transação com base em saldo, limite, risco ou outras regras.

## 🏢 Banco Adquirente

Banco adquirente é a instituição que processa o pagamento para o lojista ou empresa que está recebendo o valor.

Ele faz parte do fluxo financeiro entre o cliente, a bandeira, o banco emissor e o recebedor.

## 🔄 Clearing

Clearing, ou compensação, é a etapa em que as informações financeiras são conferidas entre as partes envolvidas na transação.

É um processo de reconciliação antes da liquidação final.

## ✅ Settlement

Settlement, ou liquidação, é a etapa em que o dinheiro é efetivamente transferido entre as instituições envolvidas.

É o momento em que a transação financeira se concretiza.

## 📒 Ledger

Ledger é um registro confiável das movimentações financeiras.

Em sistemas de pagamento, ele funciona como um livro-razão, registrando entradas, saídas e histórico das transações.

Esse componente é importante para auditoria, rastreabilidade e consistência financeira.

## 🧮 ACID

ACID é um conjunto de propriedades usadas em transações de banco de dados:

* **Atomicidade:** a transação acontece por completo ou não acontece.
* **Consistência:** os dados permanecem válidos após a transação.
* **Isolamento:** uma transação não interfere indevidamente em outra.
* **Durabilidade:** depois de confirmada, a transação permanece registrada.

Em pagamentos, essas propriedades ajudam a evitar inconsistências financeiras.

## 📊 Observabilidade

Observabilidade é a capacidade de entender o que está acontecendo dentro de um sistema a partir de dados como:

* logs;
* métricas;
* rastreamento distribuído;
* alertas.

Em sistemas distribuídos, observabilidade é essencial para investigar falhas e acompanhar o caminho de uma transação.

## 🧾 Logs

Logs são registros de eventos do sistema.

Eles ajudam a entender o que aconteceu, quando aconteceu e em qual componente.

Em uma API de pagamentos, logs podem ser usados para rastrear uma transação, investigar falhas e apoiar auditorias.

## 🧬 Correlation ID

Correlation ID é um identificador usado para acompanhar uma mesma requisição ou transação em diferentes serviços.

Em uma arquitetura com microsserviços, ele ajuda a seguir o caminho completo de uma operação.

Exemplo: uma transação passa pelo API Gateway, serviço de cliente, serviço de cobrança e banco de dados. O Correlation ID permite relacionar todos esses registros.

## 📈 Escalabilidade

Escalabilidade é a capacidade de um sistema crescer para lidar com mais acessos, transações ou volume de dados.

Em sistemas de mobilidade, isso é importante em horários de pico, eventos, feriados ou períodos de grande circulação.

## 🧯 Resiliência

Resiliência é a capacidade de um sistema continuar funcionando ou se recuperar rapidamente diante de falhas.

Em uma arquitetura de pagamentos, isso pode envolver filas, retentativas controladas, timeouts e circuit breakers.

## 🧨 Circuit Breaker

Circuit Breaker é um padrão usado para evitar que falhas se espalhem pelo sistema.

Se um serviço começa a falhar repetidamente, o Circuit Breaker interrompe temporariamente as chamadas para ele.

Isso ajuda a proteger o restante da arquitetura.

## ⏱️ Timeout

Timeout é o tempo máximo que um sistema espera por uma resposta.

Se o tempo limite for ultrapassado, a operação é encerrada ou tratada como falha.

Timeouts bem definidos evitam que requisições fiquem presas indefinidamente.

## 🔁 Retry

Retry é uma nova tentativa de executar uma operação que falhou.

Em sistemas críticos, o retry precisa ser controlado para evitar sobrecarga ou duplicidade.

Por isso, em pagamentos, retry deve ser usado junto com idempotência.

## 🧵 Fila

Fila é um mecanismo usado para armazenar mensagens ou eventos até que eles possam ser processados.

Ela ajuda a absorver picos de demanda e evita perda de dados quando algum serviço está temporariamente indisponível.

## 🧩 Desacoplamento

Desacoplamento significa reduzir a dependência direta entre componentes.

Quanto menor o acoplamento, mais fácil é alterar, escalar ou corrigir uma parte do sistema sem impactar todo o restante.

Arquiteturas orientadas a eventos ajudam bastante nesse ponto.

## 🧪 Rate Limiting

Rate limiting é o controle da quantidade de requisições que um cliente ou sistema pode fazer em determinado período.

Ele ajuda a proteger a API contra abuso, sobrecarga e ataques.

## ✅ Síntese

Os conceitos deste glossário ajudam a entender melhor como APIs podem ser projetadas para ambientes de pagamentos digitais e mobilidade.

O ponto central do estudo é que uma boa arquitetura precisa considerar não apenas o funcionamento da API, mas também segurança, consistência, rastreabilidade, resiliência e prevenção de falhas.

# Componentes do Sistema

## 📌 Objetivo

Este arquivo descreve os principais componentes de uma arquitetura conceitual para um sistema de **pagamentos digitais e mobilidade**.

O cenário considerado é o de um sistema capaz de registrar uma passagem em pedágio ou estacionamento, validar o cliente, calcular o valor, registrar a transação e gerar uma cobrança.

## 🏗️ Visão geral da arquitetura

Com base no estudo realizado no NotebookLM, o modelo mais adequado para esse cenário é uma **Arquitetura Orientada a Eventos (EDA)** apoiada por **microsserviços**.

Essa combinação permite que cada etapa do fluxo seja processada de forma mais independente, resiliente e escalável.

```text
[Sensor / Dispositivo]
        ↓
    [API Gateway]
        ↓
[Serviço de Validação]
        ↓
[Serviço de Idempotência]
        ↓
[Serviço de Cliente]
        ↓
   [Motor de Regras]
        ↓
[Serviço de Transações]
        ↓
 [Fila de Cobrança]
        ↓
[Serviço de Cobrança]
        ↓
[Gateway de Pagamento]
        ↓
 [Ledger / Banco]
        ↓
[Observabilidade]
```

## 🚗 Sensor ou dispositivo de captura

O sensor ou dispositivo é responsável por identificar o evento de mobilidade.

Exemplos:

* passagem por pedágio;
* entrada em estacionamento;
* saída de estacionamento;
* leitura de placa;
* leitura de tag;
* registro de uso de um serviço.

Esse componente atua como produtor inicial do evento.

Ele envia dados como placa, identificador da tag, horário, local e tipo de evento para a API.

## 🚪 API Gateway

O API Gateway funciona como o ponto de entrada do sistema.

Ele recebe as requisições externas e direciona para os serviços internos corretos.

Principais responsabilidades:

* receber eventos via HTTPS;
* aplicar autenticação;
* controlar autorização;
* limitar quantidade de requisições;
* rotear chamadas para os serviços internos;
* registrar logs de entrada;
* proteger os serviços internos de exposição direta.

Em um sistema crítico, o API Gateway ajuda a centralizar segurança, controle de tráfego e governança das APIs.

## ✅ Serviço de Validação

O serviço de validação verifica se os dados recebidos estão corretos e completos.

Exemplos de validação:

* formato da placa;
* identificador da tag;
* horário do evento;
* local da passagem;
* tipo de evento;
* campos obrigatórios.

Esse serviço evita que dados inválidos avancem no fluxo e causem inconsistências na cobrança ou no registro da transação.

## 🔁 Serviço de Idempotência

O serviço de idempotência é responsável por evitar duplicidade.

Em sistemas de mobilidade, sensores podem enviar o mesmo evento mais de uma vez por falha de comunicação, instabilidade ou retentativa automática.

Esse serviço verifica se uma transação semelhante já foi recebida ou processada.

Exemplo de regra:

```text
mesma placa + mesmo local + mesmo horário aproximado = possível duplicidade
```

Se o evento já tiver sido processado, o sistema não gera uma nova cobrança.

## 👤 Serviço de Cliente

O serviço de cliente identifica quem está associado ao evento.

Ele pode consultar informações como:

* cliente vinculado à tag;
* veículo cadastrado;
* status da conta;
* meio de pagamento preferencial;
* regras comerciais aplicáveis;
* elegibilidade para cobrança.

Esse componente é importante para garantir que a transação seja associada corretamente ao cliente.

## 🧮 Motor de Regras

O motor de regras calcula o valor da transação.

Esse cálculo pode considerar:

* tipo de veículo;
* local da passagem;
* tarifa vigente;
* tempo de permanência;
* descontos;
* regras comerciais;
* horário de pico;
* tipo de serviço utilizado.

Esse componente concentra a lógica de negócio relacionada ao valor que será cobrado.

## 🧾 Serviço de Transações

O serviço de transações registra a operação no sistema.

Ele mantém o histórico da transação e armazena informações como:

* identificador da transação;
* cliente;
* veículo;
* local;
* data e hora;
* valor calculado;
* status da transação;
* status da cobrança;
* identificador de correlação.

Esse serviço é essencial para consulta posterior, suporte, auditoria e rastreabilidade.

## 🧵 Fila de Cobrança

A fila de cobrança funciona como um buffer entre o registro da transação e o processamento financeiro.

Ela permite que o sistema continue recebendo eventos mesmo que o serviço de cobrança esteja lento ou temporariamente indisponível.

Principais benefícios:

* absorver picos de demanda;
* evitar perda de eventos;
* reduzir acoplamento;
* permitir processamento assíncrono;
* aumentar resiliência do fluxo.

## 💳 Serviço de Cobrança

O serviço de cobrança consome os eventos da fila e inicia o processamento financeiro.

Ele pode ser responsável por:

* preparar a solicitação de cobrança;
* acionar o gateway de pagamento;
* tratar retorno de sucesso ou falha;
* atualizar o status da transação;
* acionar retentativas controladas quando necessário.

Esse serviço deve trabalhar junto com mecanismos de idempotência para evitar cobrança duplicada.

## 🏦 Gateway de Pagamento

O gateway de pagamento é o componente que se comunica com o sistema financeiro ou instituição responsável pelo processamento do pagamento.

Ele pode realizar operações como:

* autorização;
* captura;
* confirmação;
* recusa;
* estorno;
* retorno do status do pagamento.

Em um fluxo real, esse componente precisa seguir requisitos rigorosos de segurança e confiabilidade.

## 📒 Ledger ou banco transacional

O ledger, ou banco transacional, registra as movimentações financeiras de forma confiável.

Ele é importante para garantir:

* histórico financeiro;
* rastreabilidade;
* auditoria;
* conciliação;
* consistência dos registros;
* integridade das transações.

Em sistemas de pagamento, esse componente precisa ter alto nível de confiabilidade.

## 📊 Observabilidade

A observabilidade permite acompanhar o comportamento do sistema.

Ela envolve:

* logs estruturados;
* métricas;
* rastreamento distribuído;
* alertas;
* identificadores de correlação.

Em uma arquitetura distribuída, observabilidade é essencial para entender o caminho de uma transação entre vários serviços.

Exemplo:

```text
API Gateway → Validação → Cliente → Transação → Cobrança → Pagamento
```

Sem observabilidade, encontrar a origem de uma falha pode ser muito difícil.

## 🔄 Comunicação entre os componentes

A comunicação pode acontecer de duas formas principais:

### Comunicação síncrona

Usada quando um serviço precisa de resposta imediata.

Exemplo:

```text
API Gateway consulta o serviço de cliente para validar uma conta.
```

### Comunicação assíncrona

Usada quando a operação pode continuar por eventos ou filas.

Exemplo:

```text
Transação registrada publica evento para a fila de cobrança.
```

A combinação dos dois modelos permite equilibrar resposta rápida, resiliência e escalabilidade.

## ✅ Síntese dos componentes

| Componente              | Responsabilidade principal                       |
| ----------------------- | ------------------------------------------------ |
| Sensor / Dispositivo    | Capturar o evento de mobilidade                  |
| API Gateway             | Receber, proteger e rotear requisições           |
| Serviço de Validação    | Validar estrutura e consistência dos dados       |
| Serviço de Idempotência | Evitar duplicidade de eventos ou cobranças       |
| Serviço de Cliente      | Identificar cliente, veículo e meio de pagamento |
| Motor de Regras         | Calcular valor da transação                      |
| Serviço de Transações   | Registrar operação e manter histórico            |
| Fila de Cobrança        | Desacoplar registro e processamento financeiro   |
| Serviço de Cobrança     | Processar a cobrança                             |
| Gateway de Pagamento    | Integrar com sistema financeiro                  |
| Ledger / Banco          | Registrar movimentações e garantir auditoria     |
| Observabilidade         | Monitorar, rastrear e diagnosticar falhas        |

## ✅ Conclusão

A arquitetura proposta separa responsabilidades entre componentes especializados.

Essa separação ajuda a tornar o sistema mais organizado, escalável e resiliente.

Em um cenário de pagamentos digitais e mobilidade, os componentes mais críticos são o serviço de idempotência, o serviço de transações, o serviço de cobrança, o ledger e a camada de observabilidade.

Eles ajudam a evitar cobranças duplicadas, manter histórico confiável, lidar com falhas e garantir rastreabilidade ponta a ponta.

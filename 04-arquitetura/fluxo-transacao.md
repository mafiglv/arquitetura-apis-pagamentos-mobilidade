# Fluxo de Transação

## 📌 Objetivo

Este arquivo descreve o fluxo conceitual de uma transação em um sistema de **pagamentos digitais e mobilidade**.

O cenário usado como referência é uma passagem em pedágio ou estacionamento, onde o sistema precisa capturar o evento, validar o cliente, calcular o valor, registrar a transação e gerar uma cobrança.

## 🧭 Visão geral do fluxo

O fluxo foi pensado para representar uma operação crítica, em que não basta apenas receber um evento e cobrar o cliente.

É necessário garantir que:

* os dados recebidos sejam válidos;
* o cliente seja identificado corretamente;
* a mesma passagem não seja cobrada duas vezes;
* o valor seja calculado conforme as regras de negócio;
* a transação seja registrada;
* a cobrança seja processada com segurança;
* o histórico possa ser consultado depois;
* falhas possam ser rastreadas.

## 🔁 Fluxo simplificado

```text
Veículo / Cliente
      ↓
Sensor ou dispositivo de captura
      ↓
API Gateway
      ↓
Validação dos dados
      ↓
Verificação de duplicidade
      ↓
Identificação do cliente
      ↓
Cálculo do valor
      ↓
Registro da transação
      ↓
Fila de cobrança
      ↓
Processamento da cobrança
      ↓
Gateway de pagamento
      ↓
Atualização do status
      ↓
Histórico e auditoria
```

## 1. 🚗 Captura do evento

O fluxo começa quando um evento de mobilidade é gerado.

Exemplos:

* veículo passa por um pedágio;
* veículo entra em um estacionamento;
* veículo sai de um estacionamento;
* tag é lida por um sensor;
* placa é identificada por câmera;
* uso de serviço é registrado por um dispositivo.

Nesse momento, o sistema recebe dados como:

* placa;
* identificador da tag;
* local;
* data e hora;
* tipo de evento;
* identificador do dispositivo;
* sentido da passagem ou operação realizada.

## 2. 🚪 Entrada pelo API Gateway

O evento é enviado para o **API Gateway**, que funciona como ponto de entrada da arquitetura.

Nessa etapa, o gateway pode:

* receber a requisição via HTTPS;
* validar autenticação;
* aplicar regras de autorização;
* limitar volume de chamadas;
* registrar logs de entrada;
* encaminhar a requisição para o serviço correto.

O API Gateway evita que os serviços internos fiquem expostos diretamente.

## 3. ✅ Validação dos dados

Depois da entrada pelo gateway, o evento passa por uma validação inicial.

O objetivo é verificar se os dados mínimos estão corretos.

Exemplos de validação:

* placa em formato válido;
* tag informada;
* local conhecido;
* data e hora presentes;
* tipo de evento aceito;
* dispositivo autorizado.

Se os dados forem inválidos, o evento pode ser rejeitado ou enviado para análise.

## 4. 🔁 Verificação de duplicidade

Antes de seguir para cobrança, o sistema precisa verificar se aquele evento já foi recebido ou processado.

Essa etapa está ligada ao conceito de **idempotência**.

Exemplo de possível duplicidade:

```text
mesma placa + mesmo local + mesmo intervalo de tempo
```

Se o evento for duplicado, o sistema não deve gerar uma nova cobrança.

Essa etapa é crítica para evitar que o cliente seja cobrado duas vezes por uma mesma passagem.

## 5. 👤 Identificação do cliente

Após validar que o evento é único, o sistema identifica o cliente relacionado à placa ou tag.

Essa etapa pode consultar:

* cadastro do veículo;
* conta do cliente;
* meio de pagamento associado;
* status da conta;
* situação contratual;
* regras comerciais aplicáveis.

Se o cliente não for encontrado ou estiver com conta inválida, o sistema pode marcar a transação como pendente, rejeitada ou encaminhada para tratamento manual.

## 6. 🧮 Cálculo do valor

Com o cliente identificado, o sistema calcula o valor da transação.

O cálculo pode considerar:

* tipo de veículo;
* praça de pedágio;
* tempo de permanência no estacionamento;
* tabela de tarifas;
* descontos;
* regras promocionais;
* horário;
* plano contratado.

Essa lógica pode ficar em um motor de regras para facilitar manutenção e evolução.

## 7. 🧾 Registro da transação

Depois do cálculo, a transação é registrada.

Esse registro deve guardar informações como:

* identificador único da transação;
* cliente;
* veículo;
* local;
* data e hora;
* valor;
* status inicial;
* dados do evento original;
* identificador de correlação.

O registro da transação cria uma base para histórico, auditoria, suporte e conciliação.

## 8. 🧵 Envio para fila de cobrança

Após registrada, a transação pode ser enviada para uma fila de cobrança.

Essa fila ajuda a desacoplar o registro da transação do processamento financeiro.

Isso é importante porque o sistema pode continuar registrando passagens mesmo que o serviço de cobrança esteja lento ou temporariamente indisponível.

A fila também ajuda a absorver picos de demanda.

## 9. 💳 Processamento da cobrança

O serviço de cobrança consome a mensagem da fila e inicia o processo financeiro.

Essa etapa pode envolver:

* montagem da solicitação de pagamento;
* envio para o gateway de pagamento;
* controle de retentativas;
* tratamento de recusas;
* atualização do status da cobrança.

Como envolve dinheiro, essa etapa também precisa respeitar idempotência.

## 10. 🏦 Integração com gateway de pagamento

O gateway de pagamento processa a transação junto ao sistema financeiro.

O retorno pode indicar:

* pagamento aprovado;
* pagamento recusado;
* falha temporária;
* timeout;
* necessidade de retentativa;
* erro definitivo.

O sistema precisa tratar cada retorno de forma adequada.

## 11. 📌 Atualização do status

Depois do retorno do pagamento, a transação deve ser atualizada.

Exemplos de status:

* registrada;
* aguardando cobrança;
* em processamento;
* paga;
* recusada;
* pendente;
* falha;
* cancelada.

Essa atualização permite que o histórico reflita a situação real da operação.

## 12. 📊 Histórico, auditoria e observabilidade

Por fim, a transação precisa ficar disponível para consulta e auditoria.

Também é importante que o sistema registre informações para observabilidade, como:

* logs estruturados;
* métricas;
* identificador de correlação;
* tempo de processamento;
* serviço onde ocorreu falha;
* status final da transação.

Em sistemas distribuídos, esses dados ajudam a rastrear o caminho completo da operação.

## ⚠️ Pontos críticos do fluxo

Os pontos mais sensíveis desse fluxo são:

* validação incorreta dos dados;
* falha na identificação do cliente;
* ausência de idempotência;
* duplicidade de cobrança;
* indisponibilidade do serviço de cobrança;
* falha no gateway de pagamento;
* perda de mensagens;
* falta de rastreabilidade;
* inconsistência entre status da transação e status da cobrança.

## ✅ Boas práticas aplicadas

Para tornar o fluxo mais confiável, algumas práticas são importantes:

* validar dados logo na entrada;
* usar API Gateway como camada de proteção;
* aplicar idempotência antes da cobrança;
* registrar transações antes do processamento financeiro;
* usar filas para desacoplar cobrança;
* manter logs estruturados;
* usar Correlation ID;
* tratar timeouts e retentativas com cuidado;
* atualizar status de forma clara;
* manter histórico auditável.

## 🧩 Fluxo com estados da transação

```text
EVENTO_RECEBIDO
      ↓
DADOS_VALIDADOS
      ↓
DUPLICIDADE_VERIFICADA
      ↓
CLIENTE_IDENTIFICADO
      ↓
VALOR_CALCULADO
      ↓
TRANSACAO_REGISTRADA
      ↓
COBRANCA_ENFILEIRADA
      ↓
COBRANCA_PROCESSADA
      ↓
STATUS_ATUALIZADO
      ↓
DISPONIVEL_PARA_CONSULTA
```

## ✅ Conclusão

O fluxo de transação mostra que uma arquitetura de pagamentos e mobilidade precisa ir além do simples recebimento de uma requisição.

Cada etapa tem uma responsabilidade específica e precisa contribuir para segurança, consistência, rastreabilidade e prevenção de falhas.

O ponto mais importante do fluxo é garantir que a transação seja registrada e processada sem duplicidade, com histórico confiável e possibilidade de auditoria.

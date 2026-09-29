# ⚡ Engenharia de Prompts e "Cicatrizes": Aplicações Distribuídas

Este documento registra a metodologia de interação, a evolução dos testes de prompt e os procedimentos de **Troubleshooting ("Cicatrizes")** no estudo do caderno de **Revisão de Desenvolvimento de Aplicações Distribuídas** dentro do Google NotebookLM.

---

## 🧪 Bateria de Testes: Da Pergunta Ingênua ao Prompt Engenheirado

### Caso de Teste 1: O Teorema CAP e o Modelo PACELC na Prática

#### ❌ Prompt v1 (Ingênuo):
```text
Explique o Teorema CAP e diga se o MongoDB é CP ou AP.
```
- **Comportamento da IA:** A IA respondeu de forma estática, afirmando que o MongoDB é simplesmente um banco "CP". 
- **Cicatriz Identificada (Simplificação Incorreta):** Em sistemas modernos de dados distribuídos, configurações como `writeConcern` e `readPreference` permitem alternar a garantia de consistência versus disponibilidade. Além disso, a resposta ignorou o comportamento do sistema quando **não** há partição de rede (que é o foco do modelo **PACELC** de Daniel Abadi).

---

#### ✅ Prompt v3 (Engenheirado - Ancoramento nos Padrões de Tanenbaum e Martin Fowler):
```text
Atue como um Engenheiro Principal de Sistemas Distribuídos.
Com base restrita nos capítulos de Consistência e Replicação do livro de Tanenbaum (DS4) e nos padrões de Martin Fowler:

1. Por que em uma rede real e distribuída a opção "CA" (Consistência + Disponibilidade pura) é considerada inviável perante o Teorema CAP?
2. Explique a extensão PACELC formulada por Daniel Abadi: qual trade-off ocorre no estado normal (Else) quando NÃO há partição de rede?
3. Compare o comportamento do Cassandra e do MongoDB perante o PACELC com citações diretas das fontes.
4. Conclua com um diagrama em formato texto ou tabela destacando a tomada de decisão.
```

- **Resposta Obtida no NotebookLM:**
  > *"Com base no Capítulo 7 de Tanenbaum (DS4) e nos ensaios de Fowler, uma rede distribuída fisicamente não pode eliminar a possibilidade de particionamento de rede (P) devido a falhas em switches, cabos, timeouts ou garbage collection [1][2]. Portanto, em caso de partição ($P$), o sistema é obrigado a escolher entre:*
  > *- **Consistência ($C$):** Recusar escritas/leituras para evitar dados divergentes em split-brain (ex: MongoDB sob maioria estrita).*
  > *- **Disponibilidade ($A$):** Aceitar escritas em ambos os lados da partição, tolerando leituras de dados desatualizados (ex: Cassandra).*
  > 
  > *O Teorema PACELC expande essa análise: **If Partition (P)**, choose Availability (A) or Consistency (C); **Else (E)**, choose **Latency (L)** or **Consistency (C)** [1][2]. Ou seja, mesmo quando o sistema está saudável e sem partições, manter consistência forte exige round-trips síncronos de consenso entre réplicas (como no Raft ou Two-Phase Commit), o que inevitavelmente **aumenta a latência** [2].*
  > 
  > *- **MongoDB:** tipicamente classificado como **PC/EC** (prioriza consistência tanto na partição quanto no estado normal).*
  > *- **Cassandra:** tipicamente classificado como **PA/EL** (prioriza disponibilidade na partição e baixíssima latência no estado normal com consistência eventual) [1][2]."*
- **Fontes Citadas:** `[1] Tanenbaum & Van Steen DS4 (Capítulo 7: Consistency & Replication)`, `[2] Martin Fowler (Patterns of Distributed Systems: Consistency Models)`.

---

### Caso de Teste 2: Consistência em Microsserviços: Two-Phase Commit (2PC) vs Padrão Saga

#### ❌ Prompt v1 (Ingênuo):
```text
Como fazer transações entre vários microsserviços?
```
- **Comportamento da IA:** A IA listou de forma genérica o Two-Phase Commit como se fosse a solução padrão para qualquer arquitetura de microsserviços.
- **Cicatriz Identificada (Inviabilidade Prática em Produção):** O 2PC é um protocolo **bloqueante** (*blocking protocol*). Se o coordenador falha na fase de *Prepare*, os nós participantes ficam travando recursos e locks de banco, derrubando a escalabilidade. O material da Microsoft Learn e de Fowler prescreve expressamente o uso de **Sagas** em nuvem.

---

#### ✅ Prompt v3 (Engenheirado com Foco em Resiliência e Trade-offs):
```text
Com base no catálogo Cloud Design Patterns da Microsoft Learn e no livro Designing Event-Driven Systems de Ben Stopford:
1. Por que o Two-Phase Commit (2PC) é desencorajado para microsserviços distribuídos em larga escala?
2. Compare detalhadamente as duas abordagens do Padrão Saga: Saga Orquestrada vs Saga Coreografada.
3. Como as Transações Compensatórias garantem a consistência eventual se um dos passos falhar no meio do fluxo?
4. Cite os trechos dos materiais que tratam do problema de isolamento na ausência de locks ACID (anomalia de leituras sujas).
```

- **Resposta Obtida no NotebookLM:**
  > *"Conforme documentado no Microsoft Cloud Design Patterns, o Two-Phase Commit (2PC) introduz acoplamento temporal severo e bloqueio de locks entre serviços independentes [1]. Se um participante se tornar lento ou o coordenador cair, todas as conexões de banco de dados permanecem presas, tornando o sistema frágil a falhas em cascata [1].*
  > 
  > *A alternativa padrão para nuvem é o **Padrão Saga**, que quebra a transação distribuída em uma sequência de transações locais em cada serviço [1][2]:*
  > *- **Saga Coreografada:** Os serviços escutam e publicam eventos de domínio de forma autônoma (via Kafka/RabbitMQ). Vantagem: Sem ponto central de acoplamento. Desvantagem: Risco de dependências cíclicas e dificuldade de rastrear fluxos complexos [2].*
  > *- **Saga Orquestrada:** Um serviço orquestrador central (State Machine) comanda explicitamente cada serviço participante. Vantagem: Fácil visualização de estado e auditoria. Desvantagem: Risco de acoplamento excessivo na lógica do orquestrador [1].*
  > 
  > *Se o passo 3 de 5 falhar (ex: falha no pagamento após reserva de estoque), o orquestrador aciona **Transações Compensatórias** reversas (estornar estoque e cancelar pedido) [1]. Como não existem locks distribuídos globais, leituras sujas podem ocorrer entre o início da saga e a compensação final, exigindo que o negócio aceite consistência eventual [1][2]."*
- **Fontes Citadas:** `[1] Microsoft Cloud Design Patterns (Compensating Transaction & Saga)`, `[2] Ben Stopford (Designing Event-Driven Systems, Cap. 6)`.

---

## 🩹 Tabela de "Cicatrizes": Troubleshooting no NotebookLM

| Desafio Encontrado (Sintoma) | Causa Raiz Identificada | Solução & Ajuste de Engenharia de Prompt |
| :--- | :--- | :--- |
| **Confusão entre Fila (RabbitMQ) e Log Append-Only (Kafka)** | Em perguntas gerais, a IA tratava RabbitMQ e Kafka como tecnologias intercambiáveis para qualquer problema. | Prompt com delimitação arquitetural: *"Exija que a resposta fundamente as diferenças usando a retenção de dados após consumo (deletar na fila vs persistir no log) com base em Stopford"*. |
| **Alucinação de "Transações 100% ACID em microsserviços desacoplados"** | Vícios conceituais de programadores formados em bancos relacionais monolíticos. | Instrução restritiva: *"Confronte a exigência de bancos independentes por microsserviço (Database-per-service) com a impossibilidade de manter ACID clássico sem 2PC"*. |
| **Respostas com jargões sem explicação do funcionamento** | Uso de termos como "Jitter", "Bulkhead" e "Outbox" sem descrever o mecanismo interno. | Solicitação obrigatória: *"Para cada padrão citado, defina: 1. Mecanismo de Ação; 2. Problema de Produção evitado; 3. Exemplo em código/fluxo"* |

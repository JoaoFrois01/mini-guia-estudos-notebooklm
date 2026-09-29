# 📚 Curadoria de Fontes: Caderno de Aplicações Distribuídas

Para alimentar o caderno temático de **Revisão de Desenvolvimento de Aplicações Distribuídas** no Google NotebookLM ([Acessar Caderno](https://notebook.google.com/notebook/41e49dc5-f5e8-4b07-92ef-5c995a6fa3aa?authuser=4)), foi realizada uma curadoria criteriosa de **4 fontes de referência técnica da indústria e academia**.

O critério de seleção priorizou:
- Padrões de arquitetura consolidados pelo mercado corporativo global.
- Discussão técnica profunda de trade-offs de consistência, latência e particionamento de redes.
- Disponibilidade pública aberta e gratuita para leitura e aprendizado contínuo.

---

## 📑 Fontes Selecionadas e Integradas ao Corpus

### 1. Distributed Systems (4th Edition, 2023)
- **Autores:** Maarten van Steen e Andrew S. Tanenbaum.
- **Instituição / Licença:** Publicado digitalmente de forma gratuita pelos autores sob licença educacional aberta.
- **Formato Integrado:** Livro digital completo em PDF.
- **Link Oficial:** [Distributed Systems 4th Edition - Site Oficial](https://www.distributed-systems.net/index.php/books/ds4/)
- **Critério de Escolha:** É o livro-texto canônico de sistemas distribuídos no mundo. Traz definições matemáticas e conceituais indispensáveis sobre as falácias da computação distribuída, modelos de consistência (linearizabilidade, consistência sequencial, eventual), sincronização de relógios físicos e lógicos (Lamport), e algoritmos de consenso.
- **Capítulos Prioritários no NotebookLM:**
  - *Chapter 1: Introduction* (Conceito de sistema distribuído, metas e falácias de rede).
  - *Chapter 4: Communication* (RPC, Message-Oriented Middleware, Publish-Subscribe).
  - *Chapter 7: Consistency and Replication* (Modelos de consistência data-centric e client-centric).
  - *Chapter 8: Fault Tolerance* (Confiabilidade, modelo de falhas de nós e partições de rede).

---

### 2. Cloud Design Patterns (Microsoft Azure Architecture Center)
- **Autores:** Microsoft Patterns & Practices Team / Microsoft Learn.
- **Instituição / Licença:** Microsoft Documentation / Open Access (Creative Commons Attribution 4.0).
- **Formato Integrado:** Guias arquiteturais e documentações técnicas em PDF e Markdown.
- **Link Oficial:** [Microsoft Learn - Cloud Design Patterns](https://learn.microsoft.com/en-us/azure/architecture/patterns/)
- **Critério de Escolha:** É o principal catálogo corporativo de soluções para os problemas clássicos de nuvem e microsserviços. Fornece o padrão prescritivo para resiliência e estabilidade em produção.
- **Padrões Prioritários no NotebookLM:**
  - *Circuit Breaker Pattern* (Mecanismo de proteção contra degradação em cascata).
  - *Retry Pattern com Exponential Backoff e Jitter* (Tratamento de falhas transitórias).
  - *Bulkhead Pattern* (Isolamento de pools de conexões e recursos críticos).
  - *Compensating Transaction & Saga Pattern* (Gestão de transações em bancos desacoplados).
  - *Event Sourcing e CQRS* (Separação entre modelos de comando e leitura).

---

### 3. Patterns of Distributed Systems
- **Autores:** Martin Fowler e Unmesh Joshi.
- **Instituição / Licença:** MartinFowler.com / Material aberto para a comunidade de engenharia.
- **Formato Integrado:** Artigos técnicos aprofundados e diagramas arquiteturais.
- **Link Oficial:** [Martin Fowler - Patterns of Distributed Systems](https://martinfowler.com/articles/patterns-of-distributed-systems/)
- **Critério de Escolha:** Martin Fowler é uma das maiores referências vivas em engenharia de software corporativa. Os artigos dessa série documentam o funcionamento interno de sistemas como etcd, ZooKeeper, Raft e Kafka, explicando como eles garantem replicação consistente e durabilidade de dados.
- **Padrões Prioritários no NotebookLM:**
  - *Write-Ahead Log (WAL)* (Persistência e recuperação de nós após crash).
  - *Leader and Followers* (Topologia mestre-trabalhador para garantia de ordenação de escrita).
  - *High-Water Mark* (Garantia de que réplicas sincronizadas estão atualizadas).
  - *Two-Phase Commit (2PC)* (Protocolo clássico de consenso transacional atômico).

---

### 4. Designing Event-Driven Systems
- **Autor:** Ben Stopford.
- **Instituição / Licença:** O'Reilly Media / Confluent Open Ebook Series (Distribuição gratuita).
- **Formato Integrado:** Livro digital em PDF.
- **Link Oficial:** [Confluent Books - Designing Event-Driven Systems](https://www.confluent.io/resources/ebook/designing-event-driven-systems/)
- **Critério de Escolha:** Desmistifica a virada de paradigma entre comunicação síncrona (REST/gRPC) e a Arquitetura Orientada a Eventos (EDA). Explica a estrutura de log distribuído append-only do Apache Kafka, semânticas de entrega e processamento com streams.
- **Capítulos Prioritários no NotebookLM:**
  - *Chapter 1-2: Events and the Asynchronous Enterprise*.
  - *Chapter 4: The Log - A Fundamental Concept in Distributed Systems*.
  - *Chapter 6: Event Sourcing, CQRS and the Stateful Streaming Pattern*.

---

## 📊 Matriz de Cobertura Curatorial

| Tópico de Sistemas Distribuídos | Tanenbaum (DS4) | Microsoft Cloud | Fowler & Joshi | Confluent / Stopford | Nível de Cobertura |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Fundamentos & Falácias de Rede** | ✅ Primário | ✅ Secundário | ➖ | ➖ | 100% |
| **Teorema CAP & PACELC** | ✅ Primário | ✅ Aplicação | ✅ Teórico | ✅ Prático | 100% |
| **Comunicação: RPC / gRPC / REST** | ✅ Primário | ✅ Prático | ➖ | ➖ | 100% |
| **Mensageria & EDA (Kafka / RabbitMQ)** | ✅ Conceitual | ✅ Padrões | ➖ | ✅ Especialista | 100% |
| **Transações Distribuídas (2PC vs Saga)** | ✅ Teórico | ✅ Prescritivo | ✅ Padrões | ✅ Event-Driven | 100% |
| **Padrões de Resiliência (Circuit Breaker)**| ➖ | ✅ Primário | ➖ | ✅ Secundário | 100% |
| **Observabilidade & Tracing** | ✅ Secundário | ✅ Primário | ➖ | ✅ Prático | 95% |

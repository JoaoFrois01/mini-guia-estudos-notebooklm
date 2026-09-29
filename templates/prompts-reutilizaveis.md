# 🛠️ Biblioteca de Prompts Reutilizáveis para NotebookLM

Este guia reúne um conjunto de **templates de prompts estratégicos** projetados especificamente para extrair o potencial máximo do **Google NotebookLM**. O NotebookLM opera sobre um modelo estrito de ancoragem (*grounding*), o que significa que prompts bem construídos forçam a IA a cruzar informações entre fontes anexadas, apontar referências exatas e evitar respostas genéricas da web.

---

## 🎯 Índice dos Templates

1. [Template 1: Tutor Socrático e Desafio Gradual](#template-1-modo-tutor-socrático-e-desafio-gradual)
2. [Template 2: Matriz Comparativa de Arquitetura e Trade-offs](#template-2-matriz-comparativa-de-arquitetura-e-trade-offs)
3. [Template 3: Gerador de Flashcards e Teste Ativo de Retenção](#template-3-gerador-de-flashcards-e-teste-ativo-de-retenção)
4. [Template 4: Resumo Executivo para Tomada de Decisão (Briefing)](#template-4-resumo-executivo-para-tomada-de-decisão-briefing)
5. [Template 5: Estudo de Caso Prático e Resolução de Problemas](#template-5-estudo-de-caso-prático-e-resolução-de-problemas)
6. [Template 6: Auditoria de Grounding e Validação Estrita de Fontes](#template-6-auditoria-de-grounding-e-validação-estrita-de-fontes)

---

## Template 1: Modo Tutor Socrático e Desafio Gradual

> **Objetivo:** Transformar o NotebookLM em um professor particular que não apenas entrega a resposta pronta, mas testa seu raciocínio crítico através de perguntas progressivas.

```text
Atue como um Tutor Especialista no tópico [INSERIR TÓPICO, ex: Teorema de Bayes / Teorema CAP].
Com base exclusiva no material anexado neste caderno:

1. Faça uma introdução concisa do conceito em no máximo 2 parágrafos.
2. Formule uma pergunta conceitual desafiadora para testar meu entendimento prático.
3. Não me forneça a resposta imediatamente. Peça para que eu responda antes de avançar para o próximo nível.
4. Ao avaliar minha resposta futura, aponte a página ou seção da fonte que fundamenta a correção.
```

---

## Template 2: Matriz Comparativa de Arquitetura e Trade-offs

> **Objetivo:** Comparar tecnologias, padrões ou formulações matemáticas com foco em vantagens, desvantagens e cenários de uso recomendados.

```text
Atue como um Arquiteto de Software / Especialista em Dados.
Consulte as fontes carregadas e compare detalhadamente [TECNOLOGIA/CONCEITO A, ex: Kafka / Média Amostral] e [TECNOLOGIA/CONCEITO B, ex: RabbitMQ / Mediana].

Estruture a resposta obrigatoriamente no seguinte formato:
1. Tabela Comparativa Markdown contendo as colunas: Critério | [Item A] | [Item B] | Citação da Fonte.
   - Critérios mínimos: Mecanismo Fundamental, Garantias/Propriedades, Sensibilidade a Outliers/Falhas, Caso de Uso Ideal, Contraindicação.
2. Síntese dos Trade-offs: O que ganhamos e o que perdemos ao escolher a opção A em detrimento da B?
3. Indicação exata de quais fontes anexadas embasaram cada linha da tabela.
```

---

## Template 3: Gerador de Flashcards e Teste Ativo de Retenção

> **Objetivo:** Criar cartões de memorização ativa (Active Recall) e repetição espaçada com pegadinhas conceituais reais extraídas do texto.

```text
Com base no conteúdo de [INSERIR FONTE OU CAPÍTULO, ex: Fontes de Inferência Estatística / Padrões de Resiliência]:
Gere 5 flashcards de estudo de alto nível para preparação de entrevista técnica ou concurso.

Para cada flashcard, use a seguinte estrutura:
- 📌 Frente (Pergunta Conceitual / Desafio Prático):
- 💡 Verso (Resposta Direta e Fundamentada):
- ⚠️ Pegadinha Comum (Erro frequente que profissionais cometem ao responder este ponto):
- 📖 Citação de Suporte (Trecho ou referência do material de apoio):
```

---

## Template 4: Resumo Executivo para Tomada de Decisão (Briefing)

> **Objetivo:** Sintetizar documentos extensos em um memorando técnico direto, ideal para apresentar a uma liderança ou equipe de engenharia.

```text
Atue como um Consultor Técnico Sênior. Elabore um Resumo Executivo sobre [TEMA, ex: Adoção do Padrão Saga vs 2PC / Implementação de Testes de Hipótese na Plataforma].
Restrinja-se rigorosamente às evidências das fontes anexadas.

Estrutura exigida:
1. TL;DR (Resumo em 3 tópicos de alto impacto).
2. Problema Central abordado pelos autores.
3. Principais Recomendações e Diretrizes encontradas nas fontes.
4. Riscos de Implementação ou Limitações Teóricas citadas.
5. Checklist de Validação Técnica (5 perguntas que a equipe deve responder antes de colocar em produção).
```

---

## Template 5: Estudo de Caso Prático e Resolução de Problemas

> **Objetivo:** Simular um incidente real de produção ou um desafio analítico de negócio para aplicar a teoria na prática.

```text
Crie um Cenário de Estudo de Caso Prático ambientado em uma empresa de tecnologia que esteja enfrentando problemas com [PROBLEMA, ex: Latência excessiva em microsserviços / Métricas de conversão inconclusivas em Teste A/B].

Em seguida:
1. Descreva os sintomas e os dados observados pelo time.
2. Apresente 3 hipóteses diagnósticas com base nas fontes anexadas neste caderno.
3. Forneça o plano de ação passo a passo recomendado pela literatura presente nas fontes para mitigar o problema de forma definitiva.
4. Aponte quais princípios teóricos das fontes garantem o sucesso dessa solução.
```

---

## Template 6: Auditoria de Grounding e Validação Estrita de Fontes

> **Objetivo:** Evitar alucinações da IA e checar se uma afirmação específica é realmente corroborada pela literatura carregada no NotebookLM.

```text
Quero validar a seguinte afirmação técnica: "[INSERIR AFIRMAÇÃO, ex: Um p-valor menor que 0.05 prova que o efeito é grande e importante / O Apache Kafka é um message broker AMQP]".

Avalie a afirmação confrontando-a estritamente com os documentos anexados neste caderno:
1. Veredito: A afirmação é [Totalmente Correta / Parcialmente Correta / Falsa / Inconclusiva nas fontes].
2. Justificativa Teórica: Explique por quê, destacando eventuais ambiguidades ou confusões conceituais.
3. Citações Diretas: Transcreva os trechos ou mencione as seções exatas das fontes que apoiam seu veredito.
4. Correção sugerida: Caso esteja errada ou incompleta, reformule a frase para torná-la 100% rigorosa segundo as fontes.
```

---

## 💡 Dicas de Ouro para Engenharia de Prompts no NotebookLM

1. **Evite perguntas monossilábicas ou amplas demais:** Em vez de *"Fale sobre normalidade"*, use *"Explique como o Teorema Central do Limite justifica a presença da Distribuição Normal em medições de latência de software"*.
2. **Utilize a técnica de Delimitação de Escopo:** Indique quais fontes você quer que a IA priorize (ex.: *"Consulte prioritariamente o guia da Microsoft Learn e o livro de Tanenbaum"*).
3. **Solicite Citações:** O NotebookLM possui o recurso nativo de criar notas de rodapé interativas (`[1]`, `[2]`). Exigir a citação no prompt estimula o modelo a fundamentar cada parágrafo diretamente no texto.
4. **Alterne entre Síntese e Profundidade:** Utilize o painel de chat para diálogos socráticos e a opção de "Criar Guia de Estudo / Criar Resumo" para visões gerais consolidadas.

# ⚡ Engenharia de Prompts e "Cicatrizes": Caderno de Estatística

Este documento detalha o processo experimental de interação com o **Google NotebookLM** durante o estudo do caderno de **Revisão de Estatística**. 

Diferente de um modelo generativo convencional (que responde com base em dados genéricos da internet), o NotebookLM opera com **Grounding Estrito**: ele sintetiza respostas baseando-se exclusivamente no corpus de documentos fornecido, gerando notas de rodapé interativas e citações verificáveis.

---

## 🧪 Bateria de Testes: Da Pergunta Ingênua ao Prompt Engenheirado

### Caso de Teste 1: Diferença entre Desvio Padrão Amostral e Populacional (Correção de Bessel)

#### ❌ Prompt v1 (Ingênuo):
```text
Qual a diferença entre variância e desvio padrão?
```
- **Comportamento da IA:** A IA respondeu de forma genérica e simplificada, afirmando apenas que *"o desvio padrão é a raiz quadrada da variância"*. Não explicou a razão matemática das unidades de medida, nem tocou no ponto crítico da divisão por $n-1$ versus $N$.
- **Diagnóstico:** O prompt não exigiu fundamentação teórica nem definiu a persona, resultando em um resumo raso de ensino fundamental.

---

#### ⚠️ Prompt v2 (Intermediário):
```text
Explique as fórmulas de variância e desvio padrão com base no material anexado do OpenStax e do IME-USP.
```
- **Comportamento da IA:** A IA listou as fórmulas matemáticas de $\sigma^2$, $\sigma$, $s^2$ e $s$. Citou as fontes `[1]` e `[2]`, mas ainda não explicou o motivo conceitual do porquê usamos $n-1$ na amostra (graus de liberdade).

---

#### ✅ Prompt v3 (Engenheirado - Persona + Grounding + Aplicação Prática):
```text
Atue como um Professor Universitário de Estatística e Ciência de Dados.
Com base restrita nos capítulos de Estatística Descritiva do OpenStax e do IME-USP anexados:

1. Explique conceitualmente e dimensionalmente por que calculamos o Desvio Padrão além da Variância.
2. Demonstre por que no cálculo amostral dividimos por (n - 1) em vez de n (Correção de Bessel e estimador não viesado).
3. Conecte esse conceito com um exemplo prático em Engenharia de Software (ex: análise de variabilidade de latência de microsserviços - p95 e p99).
4. Indique as citações exatas das fontes anexadas para cada ponto.
```

- **Resposta Obtida no NotebookLM:**
  > *"O cálculo do Desvio Padrão surge da necessidade de trazer a dispersão para a mesma unidade de medida dos dados originais [1], uma vez que a Variância eleva os desvios ao quadrado (resultando em unidades quadráticas, como $ms^2$) [1].*
  > 
  > *Em relação ao denominador amostral, a divisão por $(n - 1)$ — conhecida como Correção de Bessel — é necessária porque os desvios amostrais são medidos em relação à média amostral $ar{x}$, e não à verdadeira média populacional $\mu$ [2]. Como a média amostral já minimiza a soma dos quadrados dos resíduos para aquela amostra específica, dividir simplesmente por $n$ subestimaria sistematicamente a dispersão da população (estimador viesado). Perde-se 1 grau de liberdade ao fixar a média amostral [1][2].*
  > 
  > *Na Engenharia de Software, ao medir a latência de uma API em uma amostra de 100 requisições, a variância amostral com $s = \sqrt{\frac{\sum (x_i - \bar{x})^2}{n-1}}$ garante que não subestimemos o risco de caudas longas (tail latency). Um desvio padrão alto alerta que, embora a média de resposta seja 50ms, requisições nos percentis p95 e p99 sofrerão variações extremas [3]."*
- **Fontes Citadas:** `[1] OpenStax Cap. 2 (Descriptive Statistics)`, `[2] IME-USP Módulo 2`, `[3] NIST Handbook Section 1.3.5`.

---

### Caso de Teste 2: A Falácia do $p$-valor e Tomada de Decisão em Testes A/B

#### ❌ Prompt v1 (Ingênuo):
```text
O que significa um p-valor menor que 0.05?
```
- **Comportamento da IA:** A resposta inicial continha uma formulação ambígua: *"Significa que há 95% de chance de o resultado estar certo e menos de 5% de chance de ser por acaso"*.
- **Cicatriz Identificada (Alucinação Clássica):** Dizer que o $p$-valor é a "probabilidade da hipótese ser verdadeira ou falsa" é o erro mais comum em estatística. O grounding estrito precisava corrigir isso.

---

#### ✅ Prompt v3 (Refinado com Verificação Cruzada NIST / MIT):
```text
Com base estrita nas seções de Testes de Hipótese do NIST Handbook e nas notas do MIT 18.05:
1. Qual é a definição matematicamente rigorosa de p-valor sob a hipótese nula H0?
2. Por que é tecnicamente incorreto afirmar que "o p-valor é a probabilidade da hipótese nula ser verdadeira"?
3. Explique a relação de compromisso entre o Erro Tipo I (falso positivo, alfa) e o Erro Tipo II (falso negativo, beta) em um Teste A/B de software.
4. Forneça o trecho ou citação correspondente.
```

- **Resposta Obtida no NotebookLM:**
  > *"De acordo com o NIST Handbook e as notas do MIT 18.05, o p-valor é definido rigorosamente como: a probabilidade de se obter uma estatística de teste igual ou mais extrema do que a observada na amostra, assumindo que a hipótese nula ($H_0$) seja verdadeira [1][2]. Matematicamente: $P(\text{dados ou mais extremos} \mid H_0)$.*
  > 
  > *É um erro grave afirmar que o p-valor mede $P(H_0 \mid \text{dados})$, pois isso exigiria uma probabilidade a priori bayesiana [2]. O p-valor não avalia a veracidade da hipótese, mas quão incompatíveis os dados observados são com o modelo de $H_0$ [1].*
  > 
  > *Em um Teste A/B de um novo botão de checkout:*
  > *- **Erro Tipo I (Alfa, $\alpha$):** Rejeitar $H_0$ quando ela é verdadeira. Na prática: afirmar que o novo layout aumentou conversões quando na verdade não houve efeito (adotar uma mudança inútil com custo de deploy) [1].*
  > *- **Erro Tipo II (Beta, $\beta$):** Não rejeitar $H_0$ quando ela é falsa. Na prática: descartar uma melhoria real por falta de poder estatístico amostral [2].*
  > *Reduzir $\alpha$ arbitrariamente eleva $\beta$, a menos que aumentemos o tamanho da amostra $n$ [1][2]."*
- **Fontes Citadas:** `[1] NIST Handbook 1.3.5`, `[2] MIT OCW 18.05 Reading 17`.

---

## 🩹 Tabela de "Cicatrizes": Troubleshooting no NotebookLM

| Desafio Encontrado (Sintoma) | Causa Raiz Identificada | Solução & Ajuste de Engenharia de Prompt |
| :--- | :--- | :--- |
| **Respostas com fórmulas em LaTeX desconfiguradas** | O modelo às vezes misturava formatação de texto com tags HTML ou LaTeX truncado. | Adição da instrução explícita: *"Escreva as fórmulas matemáticas em notação clara com explicação textual de cada termo antes e depois da equação"*. |
| **Mistura de convenções de notação** | O material brasileiro (USP) usa $X \sim N(\mu, \sigma^2)$ enquanto fontes americanas usam desvio padrão $N(\mu, \sigma)$. | Prompt direcionado: *"Ao citar a distribuição Normal, especifique explicitamente se o segundo parâmetro representa a variância ou o desvio padrão na fonte consultada"*. |
| **Respostas excessivamente prolixas** | Documentos com mais de 300 páginas faziam o modelo trazer contextualizações históricas desnecessárias. | Imposição de restrição de formato: *"Responda em formato de tabela de 4 colunas: Conceito, Fórmula, Interpretação Prática e Citação"* ou delimitação por número de tópicos. |
| **Respostas superficiais em Teorema Central do Limite** | Perguntas curtas resultavam apenas na repetição do enunciado básico. | Estruturação de prompt solicitando o comportamento sob distribuições originais assimétricas (ex.: Exponencial/Pareto) e número mínimo de amostras ($n \ge 30$). |

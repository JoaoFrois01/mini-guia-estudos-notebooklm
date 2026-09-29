# 📚 Curadoria de Fontes: Caderno de Revisão de Estatística

Para alimentar o caderno temático de **Revisão de Estatística** no Google NotebookLM ([Acessar Caderno](https://notebook.google.com/notebook/82a3d108-fbb7-418f-9ff6-beb5de0319f9?authuser=4)), foi realizada uma curadoria rigorosa de **4 fontes abertas, acadêmicas e de padrão internacional**.

O critério de seleção priorizou materiais com:
- Rigor matemático balanceado com intuição prática.
- Exemplos voltados para análise de dados, computação e tomada de decisão.
- Licenças abertas (Open Access, Creative Commons ou Domínio Público governamental).

---

## 📑 Fontes Selecionadas e Integradas ao Corpus

### 1. Introductory Statistics 2e (OpenStax)
- **Autores:** Barbara Illowsky, Ph.D. e Susan Dean (De Anza College).
- **Instituição / Licença:** Rice University / Creative Commons Attribution License 4.0 (CC BY 4.0).
- **Formato Integrado:** Livro digital em PDF (Upload dos capítulos fundamentais).
- **Link Oficial:** [OpenStax Introductory Statistics 2e](https://openstax.org/details/books/introductory-statistics-2e)
- **Critério de Escolha:** É um dos livros-texto abertos mais consagrados do mundo acadêmico. Possui explicações didáticas sobre medidas de tendência central, dispersão, probabilidade e intervalos de confiança com notação padronizada.
- **Capítulos Prioritários no NotebookLM:**
  - *Chapter 2: Descriptive Statistics* (Variância, Desvio Padrão Amostral vs Populacional).
  - *Chapter 3: Probability Topics* (Regra da Adição, Multiplicação e Independência).
  - *Chapter 7: The Central Limit Theorem* (Teorema Central do Limite e distribuições amostrais).
  - *Chapter 9: Hypothesis Testing with One Sample* (Formulação de $H_0$, $H_1$, nível de significância $lpha$ e $p$-valor).

---

### 2. Noções de Probabilidade e Estatística (IME-USP)
- **Autores:** Marcos Nascimento Magalhães e Carlos Alberto de Bragança Pereira.
- **Instituição / Licença:** Instituto de Matemática e Estatística da Universidade de São Paulo (IME-USP) / Material Didático Aberto para Graduação.
- **Formato Integrado:** Notas de aula e apostilas abertas em PDF.
- **Link Oficial:** [Apostilas e Notas de Aula IME-USP](https://www.ime.usp.br/~jms/ensino/mae0219/)
- **Critério de Escolha:** Traz a perspectiva da escola matemática brasileira, com precisão conceitual impecável na diferenciação entre distribuições discretas (Binomial, Poisson) e contínuas (Normal, Exponencial), além de exercícios práticos de inferência.
- **Capítulos Prioritários no NotebookLM:**
  - *Módulo 2: Variáveis Aleatórias Discretas e Modelos Probabilísticos*.
  - *Módulo 4: Variáveis Contínuas e a Distribuição Normal*.
  - *Módulo 6: Introdução à Inferência Estatística e Intervalos de Confiança*.

---

### 3. NIST/SEMATECH e-Handbook of Statistical Methods
- **Instituição:** National Institute of Standards and Technology (NIST) / U.S. Department of Commerce.
- **Licença:** Domínio Público (Public Domain - U.S. Government Work).
- **Formato Integrado:** Páginas web e seções técnicas exportadas em PDF.
- **Link Oficial:** [NIST/SEMATECH Engineering Statistics Handbook](https://www.itl.nist.gov/div898/handbook/)
- **Critério de Escolha:** Referência mundial em engenharia da qualidade, telemetria e análise de confiabilidade. Essencial para conectar a teoria estatística com métricas de sistemas, detecção de outliers e testes de hipótese aplicados à engenharia.
- **Seções Prioritárias no NotebookLM:**
  - *Section 1.3.5: Quantitative Techniques* (Testes t de Student, Testes de Normalidade).
  - *Section 1.3.3: Graphical Techniques* (Boxplots, Histogramas, Quantile-Quantile Plots).
  - *Section 1.3.6: Probability Distributions* (Distribuições extremas e confiabilidade).

---

### 4. MIT OpenCourseWare: Introduction to Probability and Statistics (18.05)
- **Autores:** Jeremy Orloff e Jonathan Bloom.
- **Instituição / Licença:** Massachusetts Institute of Technology (MIT) / Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International.
- **Formato Integrado:** Lecture Notes e Reading Materials em PDF.
- **Link Oficial:** [MIT OCW 18.05](https://ocw.mit.edu/courses/18-05-introduction-to-probability-and-statistics-spring-2014/)
- **Critério de Escolha:** Aborda a transição entre o pensamento frequentista clássico e o pensamento bayesiano, muito utilizado em aprendizado de máquina, redes neurais e modelagem preditiva em sistemas de informação.
- **Tópicos Prioritários no NotebookLM:**
  - *Class 3-5: Conditional Probability, Bayes Theorem & Base Rate Fallacy*.
  - *Class 11-13: Central Limit Theorem and Law of Large Numbers*.
  - *Class 17-19: Bayesian Updating with Discrete and Continuous Priors*.

---

## 📊 Matriz de Cobertura Curatorial

| Tópico Estatístico | OpenStax | IME-USP | NIST Handbook | MIT OCW | Nível de Cobertura |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Estatística Descritiva & Dispersão** | ✅ Primário | ✅ Secundário | ✅ Prático | ➖ | 100% |
| **Probabilidade & Teorema de Bayes** | ✅ Básico | ✅ Teórico | ➖ | ✅ Avançado | 100% |
| **Distribuições (Normal, Poisson, etc.)** | ✅ Primário | ✅ Primário | ✅ Aplicação | ✅ Teórico | 100% |
| **Teorema Central do Limite (TCL)** | ✅ Primário | ✅ Secundário | ✅ Prático | ✅ Rigoroso | 100% |
| **Testes de Hipótese & p-valor** | ✅ Primário | ✅ Secundário | ✅ Engenharia | ✅ Crítico | 100% |
| **Regressão Linear & Correlação** | ✅ Primário | ✅ Secundário | ✅ Diagnóstico | ➖ | 95% |

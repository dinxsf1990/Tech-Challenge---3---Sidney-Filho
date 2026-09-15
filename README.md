# Tech Challenge FIAP — Fase 3 | Data Engineering & Analytics

## Análise do mercado brasileiro de Dados

Projeto desenvolvido para o **Tech Challenge — Fase 3**, com foco em **Engenharia de Dados, Big Data, Analytics, Data Visualization e Storytelling**, utilizando as três últimas edições analisadas da pesquisa **State of Data Brasil (2023, 2024 e 2025)**.

O objetivo é transformar dados brutos da pesquisa em informações estruturadas, indicadores e insights capazes de apoiar decisões estratégicas de uma instituição financeira que deseja expandir sua atuação em **Dados, Analytics e Inteligência Artificial**.

---

## 1. Objetivo do projeto

A investigação busca responder às principais questões propostas pelo Tech Challenge:

- Como está estruturado o mercado brasileiro de Dados?
- Quais perfis profissionais apresentam maior presença e valorização?
- Qual é o cenário de diversidade de gênero?
- Quais tecnologias apresentam maior adoção?
- Como a Inteligência Artificial está sendo utilizada?
- Existem diferenças entre cargos e níveis de senioridade?
- Como os profissionais estão distribuídos regionalmente?
- Quais modelos de trabalho predominam?
- Como se distribuem as faixas de remuneração entre os principais cargos?
- Quais oportunidades e desafios podem ser identificados para organizações que investem em Dados e IA?

---

## 2. Fonte dos dados

Foram analisadas as três edições mais recentes utilizadas no projeto:

- **State of Data Brasil 2023**
- **State of Data Brasil 2024**
- **State of Data Brasil 2025**

Fonte:

- Data Hackers / State of Data Brasil
- Base disponibilizada pelo Data Hackers no Kaggle

O projeto considera as diferenças de estrutura e nomenclatura existentes entre as edições e realiza a harmonização das variáveis necessárias para as análises.

---

## 3. Tecnologias utilizadas

### Processamento e análise

- Python
- Pandas
- NumPy
- PySpark
- Apache Spark
- Matplotlib
- Seaborn

### Ambiente de desenvolvimento

- Google Colab
- Jupyter Notebook

### Arquitetura proposta

- Amazon S3
- AWS Glue
- Glue Data Catalog
- Glue Jobs
- Glue Notebook e/ou Amazon Athena
- Apache Spark / PySpark
- Draw.io

---

## 4. Arquitetura e pipeline de dados

O projeto foi estruturado segundo o conceito de **Data Lake em camadas**, com separação entre dados brutos, dados tratados e informações analíticas.


<img width="362" height="741" alt="TechChallenge drawio" src="https://github.com/user-attachments/assets/37752bb0-3f00-418d-80cb-9a6ce9da85dd" />

### Bronze

A camada Bronze consolida os arquivos das três edições.

Principais etapas:

- leitura dos arquivos;
- inclusão do campo `ano_pesquisa`;
- conversão dos campos para `string`;
- resolução de incompatibilidades estruturais;
- consolidação utilizando `unionByName()`;
- preservação dos dados originais, sem aplicação de regras de negócio.

Resultado da consolidação:

- **14.005 registros**
- aproximadamente **910 colunas**

### Silver

A camada Silver concentra as variáveis relevantes para a análise.

Principais campos consolidados:

- `ano_pesquisa`
- `idade`
- `genero`
- `regiao`
- `cargo`
- `modelo_trabalho`
- `uso_ia`

Transformações:

- harmonização das nomenclaturas entre as edições;
- utilização de `coalesce()` para unificação de campos equivalentes;
- conversão da idade para formato numérico;
- padronização de variáveis utilizadas nas análises.

### Gold

A camada Gold transforma os dados tratados em indicadores analíticos.

Foram desenvolvidas análises de:

- estrutura do mercado por cargo;
- diversidade de gênero;
- distribuição regional;
- modelo de trabalho;
- adoção de Inteligência Artificial;
- uso de IA por cargo;
- evolução dos principais cargos;
- senioridade;
- tecnologias mais utilizadas;
- remuneração por cargo.

---

## 5. Arquitetura AWS

A arquitetura AWS apresentada no projeto foi desenhada para atender ao modelo de pipeline proposto no Tech Challenge.

Fluxo conceitual:

```text
Dados
  |
  v
Amazon S3
  |
  v
Bronze
  |
  v
AWS Glue / Spark
  |
  v
Silver
  |
  v
AWS Glue / Spark
  |
  v
Gold
  |
  +----------> Glue Data Catalog
  |
  v
Amazon Athena
  |
  v
Analytics / DataViz
```

### Importante

A arquitetura AWS é apresentada como **arquitetura proposta/alvo**.

O processamento e a validação analítica efetivamente realizados durante o desenvolvimento deste projeto foram executados em **Python/PySpark no Google Colab**.

Portanto, este repositório não deve ser interpretado como evidência de execução integral do pipeline em Amazon S3, AWS Glue ou Amazon Athena.

O diagrama AWS representa como a solução pode ser implementada em ambiente Cloud, mantendo a mesma lógica de ingestão, processamento em Spark, organização Bronze/Silver/Gold, catalogação e consumo analítico.

---

## 6. Principais análises

### 6.1 Estrutura do mercado

A consolidação dos cargos evidencia a predominância de funções analíticas e de engenharia.

Após a padronização das nomenclaturas:

- **Analista de Dados** — aproximadamente 26% dos profissionais analisados;
- **Cientista de Dados** — aproximadamente 19%;
- **Engenheiro de Dados** — aproximadamente 18%.

Os três principais perfis concentram cerca de **63% da amostra de cargos válidos** utilizada nessa análise.

Também aparecem especializações como:

- Analytics Engineer;
- ML Engineer;
- Arquiteto de Dados;
- Business Analyst.

**Insight:** o mercado mantém forte presença de funções analíticas tradicionais, ao mesmo tempo em que apresenta especializações associadas a Engenharia de Dados, Analytics e Machine Learning.

---

## 7. Diversidade de gênero

A análise consolidada apresentou:

| Gênero | Quantidade | Participação |
|---|---:|---:|
| Masculino | 10.650 | **76,0%** |
| Feminino | 3.287 | **23,5%** |
| Outros | 68 | **0,5%** |
| **Total** | **14.005** | **100%** |

A categoria **Outros** reúne:

- `Outro`
- `Prefiro não informar`

### Insight

A amostra apresenta predominância masculina, enquanto a participação feminina corresponde a aproximadamente um quarto dos respondentes.

O resultado evidencia uma dimensão relevante para estratégias de diversidade, inclusão, atração e desenvolvimento de talentos.

---

## 8. Distribuição regional

A análise regional identificou a seguinte distribuição dos respondentes:

| Região | Respondentes |
|---|---:|
| Sudeste | 8.476 |
| Sul | 2.532 |
| Nordeste | 1.504 |
| Centro-Oeste | 906 |
| Norte | 195 |
| Distrito Federal | 1 |

O **Sudeste** concentra a maior parcela da amostra, seguido pelas regiões **Sul** e **Nordeste**.

### Insight

A concentração regional reforça a importância de considerar localização geográfica nas estratégias de contratação, mas também evidencia o potencial de modelos de trabalho flexíveis para ampliar o acesso a profissionais fora dos principais polos.

---

## 9. Modelo de trabalho

A distribuição observada na análise foi:

| Modelo | Respondentes |
|---|---:|
| 100% remoto | 5.705 |
| Híbrido flexível | 2.602 |
| Híbrido com dias fixos | 2.285 |
| 100% presencial | 2.251 |

O trabalho remoto aparece como o principal modelo observado, seguido pelas modalidades híbridas.

### Insight

A forte presença de modelos remotos e híbridos pode ampliar o universo de recrutamento para posições especializadas, reduzindo a dependência de determinados polos geográficos.

---

## 10. Senioridade

A análise de senioridade compara a composição percentual dos profissionais entre 2023, 2024 e 2025, utilizando registros válidos de cada ano.

Para 2024:

- Sênior: **41,20%**
- Pleno: **36,07%**
- Júnior: **22,73%**

Para 2025:

- Sênior: **34,31%**
- Pleno: **31,03%**
- Júnior: **20,71%**
- Especialista/Staff+: **13,95%**

### Insight

A análise de senioridade complementa a visão de cargos ao mostrar o nível de experiência dos profissionais presentes na pesquisa e permite observar mudanças na composição da força de trabalho ao longo das edições.

---

## 11. Tecnologias mais utilizadas

As tecnologias foram analisadas separadamente por categoria para evitar mistura de conceitos diferentes.

### Categorias

1. **Linguagens**
2. **Cloud**
3. **Banco de dados / Plataformas**
4. **Business Intelligence**

O ranking considera o percentual de adoção entre as respostas válidas de cada pergunta. Os denominadores podem variar entre categorias.

### Principais resultados observados

#### Linguagens

- SQL — **87,66%**
- Python — **81,78%**
- C/C++/C# — entre as linguagens com presença relevante
- R — **9,81%**
- Java — **8,11%**

#### Cloud

- AWS — **48,28%**
- Azure — **34,83%**
- GCP — **30,87%**
- On Premise / sem Cloud — **14,31%**
- Oracle Cloud — entre as opções com menor adoção

#### Banco / Plataforma

A análise identifica presença relevante de plataformas e bancos como:

- PostgreSQL
- SQL Server
- Databricks
- S3
- MySQL

#### Business Intelligence

- Microsoft Power BI — **59,02%**
- Looker — **22,55%**
- Looker Studio — **15,57%**
- Tableau — **13,63%**
- Grafana — **8,69%**

### Observação metodológica

Tecnologias como **SQL Server, SQLite e Redis** pertencem à categoria de banco/plataforma e não foram classificadas como linguagens de programação.

### Insight

Os resultados evidenciam um núcleo de competências formado por **SQL, Python, Cloud e ferramentas de BI**, acompanhado por um ecossistema diversificado de bancos, plataformas e ferramentas analíticas.

---

## 12. Inteligência Artificial

A análise de utilização de IA considerou as respostas válidas e agrupou diferentes formas de utilização.

Resultados:

| Categoria | Respondentes |
|---|---:|
| IA Gratuita | 2.089 |
| Copilot / IA para Código | 1.485 |
| IA Corporativa | 1.098 |
| IA Paga Individual | 773 |
| Não utiliza IA | 280 |
| **Total válido** | **5.725** |

### Insight

A Inteligência Artificial já apresenta presença relevante na rotina dos profissionais analisados, com destaque para ferramentas gratuitas, assistentes de código e soluções disponibilizadas pelas empresas.

A análise demonstra **adoção**, mas não mede diretamente produtividade, retorno financeiro ou causalidade.

---

## 13. Uso de IA por cargo

A análise compara a utilização de diferentes modalidades de IA entre os principais cargos:

- Analista de Dados;
- Cientista de Dados;
- Engenheiro de Dados;
- Analista de BI;
- Business Analyst;
- Analytics Engineer;
- ML Engineer.

Os indicadores foram calculados separadamente para:

- IA Gratuita;
- IA Corporativa;
- IA para Código;
- IA Paga Individual;
- Não utilização.

As categorias de uso não são necessariamente mutuamente exclusivas.

### Principais achados

- **ML Engineer** apresenta destaque na utilização de IA corporativa.
- **ML Engineer** também apresenta destaque na utilização de IA para código.
- **Analistas de BI** apresentam maior utilização relativa de IA gratuita na análise realizada.
- A não utilização de IA apresenta baixa participação nos cargos avaliados.

### Insight

A adoção de IA não ocorre de maneira uniforme entre os perfis profissionais, indicando que estratégias de capacitação e governança podem ser adaptadas às necessidades de cada função.

---

## 14. Evolução dos cargos — 2023 a 2025

A evolução dos cargos foi analisada utilizando **participação percentual por ano**, evitando que diferenças no tamanho das amostras distorcessem a comparação.

Principais perfis acompanhados:

- Analista de Dados;
- Cientista de Dados;
- Engenheiro de Dados;
- Analytics Engineer;
- ML Engineer.

### Principais achados

- Analista de Dados permanece como principal cargo.
- Ciência de Dados mantém participação relevante.
- Analytics Engineer ganha espaço.
- ML Engineer apresenta crescimento consistente.

### Insight

O mercado permanece concentrado em funções analíticas tradicionais, mas apresenta sinais de maior especialização em Engenharia, Analytics e Machine Learning.

---

## 15. Remuneração por cargo

Foi utilizado como indicador a **proporção de profissionais em faixas salariais superiores a R$ 12.000/mês**.

| Cargo | Acima de R$ 12 mil/mês |
|---|---:|
| Arquiteto de Dados | **73,7%** |
| ML Engineer | **58,9%** |
| Engenheiro de Dados | **44,1%** |
| Cientista de Dados | **43,2%** |
| Analytics Engineer | **41,9%** |
| Analista de Dados | **15,9%** |
| Analista de BI | **9,5%** |

### Observação metodológica

Esse indicador **não representa salário médio**.

Ele representa a proporção dos respondentes, entre os registros com informação salarial disponível, que se encontram em faixas superiores a R$ 12.000/mês.

A edição de 2023 não apresentou registros válidos para a variável salarial no conjunto utilizado.

### Insight

Arquitetura de Dados, Machine Learning e Engenharia de Dados apresentam maior concentração relativa nas faixas salariais superiores analisadas.

Para uma instituição financeira, esse cenário reforça a necessidade de estratégias específicas de contratação, desenvolvimento e retenção de competências críticas.

---

## 16. Principais insights

### 1. O mercado está se especializando

Além dos perfis analíticos tradicionais, funções como Analytics Engineer, ML Engineer e Arquitetura de Dados aparecem como especializações relevantes.

### 2. SQL e Python formam um núcleo técnico importante

As duas linguagens apresentam elevada adoção entre os profissionais analisados.

### 3. Cloud e BI fazem parte do ecossistema profissional

AWS, Azure, GCP e ferramentas de BI apresentam presença relevante na amostra.

### 4. IA já está presente na rotina profissional

Ferramentas gratuitas, corporativas e assistentes de código aparecem de maneira relevante entre as respostas válidas.

### 5. Competências especializadas apresentam maior concentração salarial

Os cargos analisados não apresentam a mesma concentração nas faixas superiores a R$ 12 mil/mês.

---

## 17. Recomendações estratégicas

### 1. Priorizar retenção de competências críticas

Estruturar políticas de retenção para profissionais de:

- Engenharia de Dados;
- Machine Learning;
- Arquitetura de Dados.

### 2. Estruturar capacitação em IA

Criar programas de desenvolvimento específicos por perfil profissional, combinando:

- produtividade;
- ferramentas autorizadas;
- governança;
- segurança;
- uso responsável de IA.

### 3. Ampliar o alcance do recrutamento

Utilizar modelos remotos e híbridos para ampliar o acesso a profissionais especializados fora dos principais polos geográficos.

### 4. Desenvolver competências híbridas

Combinar conhecimentos de:

**Dados + Programação + Cloud + BI + IA**

para formar profissionais capazes de atuar em diferentes etapas do ciclo de dados.

---

## 18. Limitações da análise

- Os dados são provenientes de pesquisa e representam respostas autodeclaradas.
- As perguntas possuem diferentes quantidades de respostas válidas.
- Alguns indicadores utilizam denominadores específicos para cada variável.
- A análise é predominantemente descritiva.
- Associação entre variáveis não deve ser interpretada automaticamente como causalidade.
- A análise salarial utiliza faixas de remuneração, e não salários individuais.
- Diferenças entre as estruturas das edições exigiram harmonização de campos.
- A arquitetura AWS apresentada é uma arquitetura proposta; a validação analítica foi realizada em Python/PySpark no Google Colab.
- O indicador de adoção de IA mede utilização declarada e não mede diretamente produtividade, ROI ou impacto financeiro.

---

## 19. Entregáveis do projeto

O Tech Challenge solicita uma solução que conecte arquitetura de dados, processamento, análise exploratória, DataViz e Storytelling.

Este projeto está organizado para entregar:

### Material executivo

- PowerPoint com DataViz e Storytelling;
- principais indicadores;
- análises;
- insights;
- recomendações;
- arquitetura AWS.

### Código

- Notebook `.ipynb`;
- processamento com PySpark;
- ingestão;
- tratamento;
- transformação;
- organização Bronze/Silver/Gold;
- análises;
- geração dos dados utilizados nos gráficos.

### Arquitetura

- Diagrama da solução AWS desenvolvido em Draw.io.

---

## 20. Estrutura sugerida do repositório

```text
/
├── README.md
├── Tech_Challenge_Fase3_FINAL(4).ipynb
├── dados/
│   ├── State of Data Brasil 2023
│   ├── State of Data Brasil 2024
│   └── State of Data Brasil 2025
├── graficos/
│   ├── mercado_cargos.png
│   ├── diversidade_genero.png
│   ├── distribuicao_regional.png
│   ├── modelo_trabalho.png
│   ├── adocao_ia.png
│   ├── ia_por_cargo.png
│   ├── evolucao_cargos.png
│   ├── senioridade.png
│   ├── tecnologias.png
│   └── remuneracao_cargo.png
└── arquitetura/
    └── TechChallenge.drawio.png
```

A estrutura final pode ser ajustada de acordo com a organização utilizada para a entrega.

---

## 21. Como executar

O notebook pode ser executado em ambiente compatível com Python e PySpark, incluindo Google Colab.

### Dependências principais

```python
pandas
numpy
matplotlib
seaborn
pyspark
```

### Fluxo de execução

1. Disponibilizar os arquivos das pesquisas de 2023, 2024 e 2025.
2. Inicializar o Spark.
3. Executar a ingestão das bases.
4. Construir a camada Bronze.
5. Construir a camada Silver.
6. Gerar as tabelas e indicadores Gold.
7. Executar as análises.
8. Gerar os gráficos.

---

## 22. Conclusão

A investigação demonstra como uma pesquisa de mercado pode ser transformada em uma solução analítica estruturada, conectando:

**Dados → Engenharia → Analytics → DataViz → Insights → Decisão**

Os resultados mostram um mercado brasileiro de Dados com forte presença de competências tradicionais, como SQL e Python, crescente especialização profissional, adoção relevante de Cloud e BI e presença cada vez maior da Inteligência Artificial na rotina dos profissionais.

Para uma instituição financeira, esses sinais reforçam a importância de uma estratégia integrada de **talentos, tecnologia e IA**, com foco em competências críticas, capacitação contínua, governança e ampliação do acesso ao mercado de profissionais especializados.

---

## 23. Referências

- **State of Data Brasil / Data Hackers** — pesquisas utilizadas no projeto.
- **FIAP — Tech Challenge Fase 3** — briefing e requisitos da atividade.
- **Amazon Web Services (AWS)** — serviços considerados na arquitetura proposta.
- **Apache Spark / PySpark** — processamento distribuído utilizado na implementação analítica.
- **Draw.io** — ferramenta utilizada para representação da arquitetura.

---

## Licença / finalidade

Projeto desenvolvido para fins acadêmicos no âmbito do **FIAP Tech Challenge — Fase 3**.

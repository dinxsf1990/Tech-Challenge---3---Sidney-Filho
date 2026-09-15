# Tech Challenge – Fase 3 | Data Engineering & Analytics

## 1. Sobre o projeto

Projeto desenvolvido para o **Tech Challenge – Fase 3**, com foco em Engenharia de Dados, Analytics e geração de insights a partir da pesquisa **State of Data Brasil**, considerando as edições de 2023, 2024 e 2025.

O objetivo é transformar os dados brutos da pesquisa em informações estruturadas e análises que possam apoiar decisões estratégicas, especialmente no contexto de uma **instituição financeira**.

---

## 2. Objetivos

- Consolidar os dados das pesquisas de 2023, 2024 e 2025.
- Estruturar os dados utilizando uma abordagem de camadas **Bronze, Silver e Gold**.
- Utilizar **PySpark** para processamento e transformação.
- Analisar o perfil dos profissionais de dados.
- Avaliar distribuição por cargo, gênero, região e modelo de trabalho.
- Analisar a adoção e utilização de Inteligência Artificial.
- Avaliar a evolução dos principais cargos entre 2023 e 2025.
- Relacionar cargos e faixas de remuneração.
- Gerar insights e recomendações aplicáveis ao contexto financeiro.
- Propor uma arquitetura de dados em ambiente AWS.

---

## 3. Fonte dos dados

Os dados utilizados são provenientes da pesquisa **State of Data Brasil**, realizada pela comunidade Data Hackers, considerando as edições de:

- 2023
- 2024
- 2025

Os arquivos foram tratados e consolidados no notebook deste projeto.

---

## 4. Arquitetura de dados

A arquitetura proposta segue o conceito de processamento em camadas:

```text
                    STATE OF DATA BRASIL
                         2023–2025
                              |
                              v
                         AWS S3
                              |
                              v
                    +-------------------+
                    |      BRONZE       |
                    | Dados brutos      |
                    | consolidados       |
                    +-------------------+
                              |
                              v
                    AWS Glue / PySpark
                              |
                              v
                    +-------------------+
                    |      SILVER       |
                    | Dados tratados    |
                    | e padronizados    |
                    +-------------------+
                              |
                              v
                    +-------------------+
                    |       GOLD        |
                    | Indicadores e     |
                    | análises          |
                    +-------------------+
                              |
                              v
                    Athena / DataViz
```

### Arquitetura AWS

A arquitetura apresentada no projeto considera os seguintes componentes:

- **Amazon S3** – armazenamento dos dados.
- **AWS Glue** – processamento e integração dos dados.
- **Glue Data Catalog** – catálogo e metadados.
- **PySpark / Spark** – transformação dos dados.
- **Amazon Athena** – consulta analítica.
- **Data Visualization** – apresentação dos indicadores e insights.

> **Importante:** o processamento apresentado no notebook foi executado em ambiente Google Colab utilizando PySpark. Os serviços AWS fazem parte da **arquitetura proposta** e não foram executados integralmente neste notebook.

---

## 5. Organização dos dados

### Bronze

A camada Bronze representa os dados em sua forma bruta/consolidada.

Nesta etapa:

- Os arquivos de 2023, 2024 e 2025 são carregados.
- É adicionada a identificação do ano da pesquisa.
- As estruturas são unificadas.
- Os dados são armazenados de forma consolidada.

Resultado da consolidação:

- **14.005 registros**
- **910 colunas**

---

### Silver

Na camada Silver são selecionadas e padronizadas as informações utilizadas nas análises.

Principais campos utilizados:

- Ano da pesquisa
- Idade
- Gênero
- Região
- Cargo
- Modelo de trabalho
- Uso de IA

Também são realizadas transformações de tipos e harmonização de nomes de colunas entre diferentes edições da pesquisa.

---

### Gold

A camada Gold contém as informações preparadas para análise e tomada de decisão.

Foram desenvolvidas análises relacionadas a:

- Estrutura do mercado por cargo.
- Diversidade de gênero.
- Distribuição regional.
- Modelo de trabalho.
- Adoção de Inteligência Artificial.
- Utilização de IA por cargo.
- Evolução dos principais cargos entre 2023 e 2025.
- Relação entre cargo e faixa salarial.

---

## 6. Principais análises

### Perfil profissional

A análise permite observar a composição do mercado de profissionais de dados por diferentes dimensões, como cargo, região, gênero e modelo de trabalho.

### Inteligência Artificial

A utilização de IA foi categorizada em grupos como:

- IA gratuita.
- Copilot / IA para código.
- IA corporativa.
- IA paga individualmente.
- Não utilização de IA.

A análise também considera a utilização de IA por cargo.

### Evolução dos cargos

Foi analisada a participação dos principais cargos de dados ao longo das edições de 2023, 2024 e 2025, permitindo identificar tendências de crescimento, estabilidade e transformação do mercado.

### Remuneração

Foi realizada uma análise da distribuição das faixas salariais por cargo.

Considerando a faixa de remuneração **acima de R$ 12.000/mês**, os resultados consolidados indicaram:

| Cargo | Total | Acima de R$ 12 mil | Percentual |
|---|---:|---:|---:|
| Arquiteto de Dados | 76 | 56 | 73,7% |
| ML Engineer | 209 | 123 | 58,9% |
| Engenheiro de Dados | 1.015 | 448 | 44,1% |
| Cientista de Dados | 1.111 | 480 | 43,2% |
| Analytics Engineer | 363 | 152 | 41,9% |
| Analista de Dados | 1.556 | 247 | 15,9% |
| Analista de BI | 611 | 58 | 9,5% |

Os valores devem ser interpretados como uma análise descritiva da amostra disponível para a variável salarial.

---

## 7. Principais insights

### 1. O mercado está se tornando mais especializado

Cargos como **Engenheiro de Dados, ML Engineer e Analytics Engineer** representam funções cada vez mais específicas dentro do ecossistema de dados.

### 2. IA já faz parte da rotina profissional

A presença de ferramentas de IA, especialmente ferramentas voltadas para desenvolvimento e produtividade, demonstra uma mudança no processo de trabalho dos profissionais de dados.

### 3. A remuneração varia significativamente entre os cargos

As faixas salariais mais elevadas apresentam maior concentração em funções de maior especialização técnica e arquitetural.

### 4. O modelo de trabalho tornou-se uma dimensão estratégica

A distribuição entre trabalho remoto, híbrido e presencial pode impactar políticas de contratação, retenção e organização das equipes.

### 5. A evolução do mercado exige atualização contínua

A combinação entre engenharia de dados, analytics, cloud e inteligência artificial indica a necessidade de desenvolvimento contínuo das competências profissionais.

---

## 8. Recomendações para uma instituição financeira

Com base nas análises realizadas, são propostas três frentes estratégicas:

### 1. Desenvolvimento de competências em IA

Investir em capacitação e ferramentas de IA para aumentar produtividade, automação e capacidade analítica das equipes.

### 2. Fortalecimento da engenharia de dados

Priorizar profissionais e competências relacionadas à construção de pipelines, arquitetura de dados, qualidade, governança e processamento em escala.

### 3. Estratégia de pessoas baseada em dados

Utilizar informações de mercado para apoiar decisões de contratação, remuneração, retenção e definição do modelo de trabalho.

---

## 9. Tecnologias utilizadas

### Processamento e análise

- Python
- Pandas
- NumPy
- PySpark
- Apache Spark
- Matplotlib
- Seaborn

### Ambiente

- Google Colab
- Jupyter Notebook

### Arquitetura proposta

- Amazon S3
- AWS Glue
- Glue Data Catalog
- Amazon Athena
- Draw.io

---

## 10. Estrutura do projeto

```text
/
├── Tech_Challenge_Fase3_FINAL.ipynb
├── README.md
├── dados/
│   ├── State of Data Brasil 2023
│   ├── State of Data Brasil 2024
│   └── State of Data Brasil 2025
└── arquitetura/
    └── TechChallenge.drawio.png
```

A estrutura dos arquivos pode variar conforme a organização utilizada para entrega no repositório.

---

## 11. Como executar

### 1. Abrir o notebook

O notebook pode ser executado no **Google Colab** ou em ambiente compatível com Python e PySpark.

### 2. Disponibilizar os arquivos

Os arquivos CSV das pesquisas de 2023, 2024 e 2025 devem estar disponíveis nos caminhos definidos no notebook.

### 3. Executar as células

Execute as células sequencialmente para:

1. Inicializar o Spark.
2. Carregar os dados.
3. Construir a camada Bronze.
4. Construir a camada Silver.
5. Criar as análises Gold.
6. Gerar tabelas e visualizações.
7. Avaliar os insights.

---

## 12. Entregáveis

O projeto contempla:

- Notebook de processamento e análise.
- Pipeline conceitual Bronze → Silver → Gold.
- Análises exploratórias e indicadores.
- Visualizações.
- Análise de remuneração.
- Análise de adoção de IA.
- Arquitetura de dados proposta em AWS.
- Insights e recomendações para uma instituição financeira.
- README para documentação do projeto.

---

## 13. Considerações finais

O projeto demonstra como dados de uma pesquisa de mercado podem ser transformados em informações estruturadas para apoiar decisões de negócio.

A utilização de uma arquitetura em camadas permite separar dados brutos, dados tratados e informações analíticas, criando uma estrutura compatível com ambientes modernos de Engenharia de Dados.

Os resultados também evidenciam mudanças relevantes no mercado de profissionais de dados, especialmente relacionadas à especialização das funções, remuneração, modelos de trabalho e adoção de Inteligência Artificial.

A arquitetura AWS apresentada representa uma evolução natural da solução, permitindo que o pipeline seja posteriormente operacionalizado em um ambiente cloud com maior escalabilidade, governança e capacidade de consulta.

---

## 14. Referências

- State of Data Brasil — Data Hackers.
- Documentação oficial do Apache Spark / PySpark.
- Documentação oficial da AWS — Amazon S3.
- Documentação oficial da AWS — AWS Glue.
- Documentação oficial da AWS — Amazon Athena.


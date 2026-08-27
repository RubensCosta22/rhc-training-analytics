# RHC Training Analytics

Projeto end-to-end de Engenharia de Dados, Analytics e Business Intelligence construído a partir dos dados do **RHC Training V2**, uma aplicação de treino desenvolvida e utilizada pelo próprio autor do projeto.

O objetivo é demonstrar o ciclo completo dos dados: da geração no aplicativo até o tratamento, modelagem analítica, visualização e geração de insights.

## Visão geral

Os dados são gerados pelo RHC Training V2 e armazenados no Supabase/PostgreSQL. O pipeline utiliza Python e Pandas no Google Colab para construir uma arquitetura em camadas Bronze, Silver e Gold. A camada Gold será utilizada como fonte para o Qlik Sense, onde serão desenvolvidos dashboards e análises sobre desempenho e evolução dos treinos.

```text
RHC Training V2
      |
      v
Supabase / PostgreSQL
      |
      v
Google Colab + Python
      |
      v
Bronze -> Silver -> Gold
      |
      v
Qlik Sense
      |
      v
Dashboard + Analytics
```

## Objetivos do projeto

- Construir um pipeline de dados a partir de uma aplicação real.
- Aplicar conceitos de arquitetura Medalhão (Bronze, Silver e Gold).
- Realizar limpeza, padronização e validação de dados com Python/Pandas.
- Transformar estruturas semiestruturadas, incluindo campos JSON, em dados analíticos.
- Implementar verificações de qualidade de dados.
- Construir um modelo dimensional para análise.
- Criar métricas e KPIs relacionados à evolução dos treinos.
- Desenvolver dashboards e análises no Qlik Sense.

## Tecnologias

- Supabase
- PostgreSQL
- Python
- Pandas
- Google Colab
- SQL
- Qlik Sense
- Git / GitHub

## Arquitetura de dados

### Bronze

Camada de ingestão. Preserva os dados extraídos da origem com o mínimo possível de transformação, permitindo rastreabilidade entre o banco transacional e o pipeline analítico.

### Silver

Camada responsável por qualidade e transformação dos dados, incluindo:

- conversão de tipos;
- tratamento de valores nulos;
- padronização de nomes e valores;
- tratamento de datas;
- validações de integridade;
- transformação de campos JSON;
- aplicação de regras de negócio;
- remoção ou tratamento de registros inconsistentes quando necessário.

### Gold

Camada orientada ao consumo analítico. Os dados tratados são organizados em fatos, dimensões e métricas para consumo pelo Qlik Sense.

Modelo inicial planejado:

```text
gold/
|-- dim_date
|-- dim_profile
|-- dim_exercise
|-- dim_program
|-- fact_workout
|-- fact_workout_exercise
|-- fact_exercise_set
|-- fact_body_measurement
`-- fact_program_exposure
```

## Pipeline

Os notebooks serão organizados de acordo com as etapas do processamento:

1. `01_bronze_extract.ipynb` - extração dos dados do Supabase e persistência da camada Bronze.
2. `02_silver_transform.ipynb` - limpeza, padronização e transformação.
3. `03_gold_model.ipynb` - construção das tabelas analíticas.
4. `04_data_quality.ipynb` - validações e testes de qualidade dos dados.

## Estrutura do repositório

```text
rhc-training-analytics/
|-- README.md
|-- requirements.txt
|-- .gitignore
|-- notebooks/
|-- src/
|   |-- extract/
|   |-- transform/
|   `-- utils/
|-- data/
|   |-- bronze/
|   |-- silver/
|   `-- gold/
|-- sql/
|-- qlik/
`-- docs/
    |-- architecture/
    |-- data_model/
    `-- dashboard/
```

## Análises planejadas

O dashboard final poderá explorar indicadores como:

- quantidade e frequência de treinos;
- duração média das sessões;
- volume total e volume por período;
- evolução de carga por exercício;
- recordes pessoais;
- séries e repetições executadas;
- evolução de medidas corporais;
- aderência aos programas de treino;
- RPE e progressão de carga;
- distribuição de volume por exercício e grupo muscular.

## Segurança e privacidade

O repositório não deve armazenar credenciais, chaves do Supabase, arquivos `.env`, dados pessoais sensíveis ou exports completos do banco de produção. Quando necessário, dados de demonstração deverão ser anonimizados.

## Status

🚧 Projeto em desenvolvimento.

- [x] Aplicação e banco de dados criados
- [x] Dados reais de utilização gerados
- [ ] Pipeline Bronze
- [ ] Transformações Silver
- [ ] Modelo Gold
- [ ] Testes de qualidade
- [ ] Integração com Qlik Sense
- [ ] Dashboard
- [ ] Análise e documentação dos insights

## Autor

**Rubens Costa**

Projeto desenvolvido para estudo e portfólio nas áreas de Engenharia de Dados, Analytics e Business Intelligence.

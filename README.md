# RHC Training Analytics

> **Do aplicativo ao dashboard:** dados gerados pelo uso real do RHC Training, tratados em uma arquitetura Bronze → Silver → Gold e analisados no Power BI.

O **RHC Training Analytics** nasceu de uma pergunta simples: em vez de utilizar um dataset pronto para montar um dashboard, por que não analisar os dados gerados por uma aplicação que eu mesmo desenvolvi e utilizo?

O resultado é um projeto end-to-end que conecta **produto, geração de dados, armazenamento, engenharia de dados, modelagem analítica e visualização**.

## Dashboard público

**Power BI:**  
https://app.powerbi.com/view?r=eyJrIjoiNzcwYTIzZTktNzY5Ni00ZTM1LWFkNTEtZWRkODRmYWM0MzczIiwidCI6IjUzM2FlNjZjLTI1NjktNGNjNS04YTZkLThiMDdhOWFlNzBlMyJ9

## Arquitetura

```text
RHC Training
     │
     ▼
  Supabase
     │
     ▼
   Bronze
     │
     ▼
   Silver
     │
     ▼
    Gold
     │
     ▼
   Parquet
     │
     ▼
  Power BI
```

### 1. Origem — RHC Training

O RHC Training é a aplicação que gera os dados utilizados neste projeto. Ela registra informações reais dos meus próprios treinos, incluindo sessões, exercícios, séries, repetições, cargas, volume e percepção de esforço (RPE).

A aplicação continua em uso. Por isso, o banco operacional continua recebendo novos registros mesmo quando o snapshot analítico ainda não foi reprocessado.

### 2. Bronze — ingestão

A camada Bronze preserva os dados extraídos da origem com o mínimo de transformação, mantendo uma base rastreável para as etapas seguintes.

### 3. Silver — tratamento e qualidade

A Silver organiza, tipa e valida os dados antes da modelagem analítica. Entre as verificações realizadas estão:

- consistência de chaves;
- disponibilidade das colunas de relacionamento;
- registros órfãos;
- tratamento de estruturas JSON;
- padronização necessária para consumo analítico.

### 4. Gold — modelo analítico

A Gold transforma os dados tratados em fatos e dimensões adequados para análise.

Principais entidades analíticas:

- dimensões de data, exercício, perfil e programa;
- fatos de sessões de treino;
- execuções de exercícios;
- séries;
- exposição ao programa;
- medidas corporais.

Os datasets Gold são persistidos em **Parquet** para consumo no Power BI.

## Uma decisão de modelagem

O catálogo possui exercícios que ainda não foram executados. Em vez de excluir esses registros da dimensão de exercícios, o modelo preserva o catálogo completo e adiciona indicadores de utilização.

Isso permite distinguir **“exercício existente no catálogo”** de **“exercício já realizado”** sem perder informação de referência.

## Power BI

O relatório possui duas visões principais.

### Visão Geral de Treinos

Apresenta sessões realizadas, execuções, séries, volume total, duração média, evolução do volume, frequência semanal, volume por treino e exercícios com maior volume.

### Progressão por Exercício

Permite selecionar um exercício e acompanhar carga máxima, sessões, séries, repetições, volume, progressão de carga, evolução de volume, RPE e histórico por data.

## Snapshot atual

O dashboard publicado representa um **snapshot processado** da base. Como o RHC Training continua sendo utilizado, a aplicação pode apresentar registros mais recentes que ainda não chegaram ao Power BI.

Isso é intencionalmente visível nesta primeira versão e conecta diretamente ao próximo desafio do projeto: automatizar a atualização do pipeline.

## Tecnologias

- RHC Training
- Supabase / PostgreSQL
- Python
- Pandas
- Google Colab
- Parquet
- Power BI
- Git / GitHub

## Privacidade dos dados

Os dados são provenientes do uso real do RHC Training. Arquivos brutos e informações pessoais não são publicados neste repositório.

O objetivo é demonstrar arquitetura, tratamento, modelagem, validação e resultado analítico.

## Uso de IA

IA foi utilizada como ferramenta de apoio ao desenvolvimento: discussão de alternativas, revisão de código, investigação de problemas, apoio em DAX e documentação.

As respostas não foram tratadas como resultado final automaticamente. Soluções foram testadas contra os dados, revisadas e, quando necessário, corrigidas. As decisões de arquitetura, regras, validações e implementação permaneceram parte do processo de desenvolvimento.

## Próxima etapa

A versão atual ainda possui etapas manuais entre a origem e o dashboard.

O próximo objetivo é evoluir para:

```text
RHC Training → Supabase → pipeline automatizado → Bronze/Silver/Gold → atualização do Power BI
```

A meta é reduzir intervenção manual e permitir atualizações recorrentes, sem apresentar a arquitetura atual como tempo real antes que ela efetivamente seja.

---

**Foram muitos treinos até chegar nesse dashboard. 😅**

Projeto desenvolvido como estudo prático de engenharia e análise de dados a partir de dados gerados por uma aplicação própria.

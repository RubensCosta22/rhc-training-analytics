# RHC Training Analytics

Projeto de dados criado a partir do **RHC Training**, uma aplicação de treino desenvolvida e utilizada por mim no dia a dia.

O objetivo deste repositório é documentar o caminho completo dos dados: da aplicação que gera os registros de treino até o tratamento, modelagem analítica e visualização no Power BI.

## Dashboard público

O dashboard atual pode ser acessado no Power BI:

https://app.powerbi.com/view?r=eyJrIjoiNzcwYTIzZTktNzY5Ni00ZTM1LWFkNTEtZWRkODRmYWM0MzczIiwidCI6IjUzM2FlNjZjLTI1NjktNGNjNS04YTZkLThiMDdhOWFlNzBlMyJ9

## Fluxo do projeto

```text
RHC Training
     |
     v
  Supabase
     |
     v
   Bronze
     |
     v
   Silver
     |
     v
    Gold
     |
     v
 Power BI
```

### RHC Training

O RHC Training é a aplicação que origina os dados utilizados neste projeto. Ela registra informações reais dos meus próprios treinos, como sessões realizadas, exercícios, séries, repetições, cargas, volume e RPE.

A aplicação continua em uso, portanto o conjunto de dados evolui conforme novos treinos são registrados.

### Bronze

Camada de ingestão dos dados de origem, preservando os registros com o mínimo de transformação.

### Silver

Camada destinada à limpeza, padronização, validação de relacionamentos e preparação dos dados.

Entre as verificações realizadas estão:

- consistência das chaves;
- relacionamentos entre tabelas;
- identificação de registros órfãos;
- tratamento e padronização das estruturas necessárias para análise.

### Gold

Camada analítica construída a partir das tabelas tratadas.

O modelo separa dimensões e fatos para facilitar o consumo pelas ferramentas de BI, incluindo informações de:

- datas;
- perfil;
- exercícios;
- programas de treino;
- sessões;
- execuções de exercícios;
- séries;
- progressão e exposição ao programa;
- medidas corporais.

## Power BI

O relatório foi construído sobre os arquivos Parquet da camada Gold.

Atualmente possui duas páginas principais:

### Visão Geral de Treinos

Apresenta indicadores como:

- sessões realizadas;
- execuções de exercícios;
- séries executadas;
- volume total;
- duração média;
- evolução do volume;
- frequência semanal;
- volume por treino;
- exercícios com maior volume.

### Progressão por Exercício

Permite selecionar um exercício e acompanhar:

- carga máxima;
- número de sessões;
- séries;
- repetições;
- volume;
- evolução da carga;
- evolução do volume;
- RPE ao longo do tempo;
- histórico por data.

## Tecnologias utilizadas

- RHC Training
- Supabase / PostgreSQL
- Python
- Pandas
- Google Colab
- Parquet
- Power BI
- Git / GitHub

## Sobre os dados

Os dados utilizados são provenientes do uso real do RHC Training. Os arquivos brutos e dados pessoais não são publicados neste repositório.

O foco do repositório é demonstrar a arquitetura, as transformações, a modelagem e o resultado analítico.

## Uso de IA

Ferramentas de IA foram utilizadas como apoio durante o desenvolvimento, principalmente para discussão de alternativas, revisão de código, investigação de problemas e apoio na documentação.

As decisões de implementação, testes, validações, ajustes do modelo e uso da aplicação fizeram parte do processo de desenvolvimento do projeto.

## Próximos passos

O próximo objetivo é reduzir o processo manual entre a aplicação e o BI, automatizando o pipeline para permitir atualizações recorrentes e, posteriormente, uma experiência de dados mais próxima do tempo real.

---

Projeto desenvolvido como estudo prático de engenharia e análise de dados utilizando dados gerados por uma aplicação própria.

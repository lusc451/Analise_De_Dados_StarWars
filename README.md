# Análise de Dados - Universo Star Wars

## 📖 Sobre o Projeto
Projeto de **análise de dados** e **pipeline de ETL** utilizando como dataset a [The Star Wars API (SWAPI)](https://swapi.dev/).  
O objetivo é **coletar**, **limpar**, **converter** e **analisar** dados de planetas do universo Star Wars para, por meio de **estatística descritiva** e **plotagem de gráficos**, **identificar os 10 planetas mais populosos** e suas populações.

> **Resumo:** Este repositório contém um fluxo completo de ETL (extração → transformação → carga) a partir da SWAPI, seguido de análises descritivas e visualizações que evidenciam os planetas mais populosos.

---

## ✨ Objetivos

- **ETL completo** a partir da SWAPI:
  - **Extração:** consulta paginada aos endpoints públicos.
  - **Transformação:** limpeza, padronização de tipos, tratamento de nulos e normalização de campos (por ex., `population`).
  - **Carga/Armazenamento:** salvando dados intermediários e finais (ex.: CSV/Parquet).
- **Análise descritiva**:
  - Estatísticas básicas (contagem, mínimos/máximos, distribuição, valores ausentes).
  - Filtragem/ordenação dos **Top 10 planetas por população**.
- **Visualização**:
  - **Gráfico** (ex.: barras) com os 10 planetas mais populosos.
  - Tabela final com nomes e populações.

---


## 🎯 Objetivo Final

O principal intuito deste projeto é, através da análise e da visualização de dados, responder à seguinte pergunta:

**Quais são os 10 planetas mais populosos do universo Star Wars e qual a população de cada um deles?**

O gráfico gerado ao final do processo de análise apresenta de forma clara e objetiva a resposta para essa questão, destacando os planetas que se destacam em termos de população.

---

## 🗂️ Escopo dos Dados

- **Fonte:** [SWAPI — swapi.dev](https://swapi.dev/)
- **Entidade principal:** `planets`
- **Atributos relevantes (exemplos):**
  - `name` (nome do planeta)
  - `population` (população; muitas vezes como string e podendo ser `"unknown"`)
  - `climate`, `terrain`, `gravity`, `diameter`, etc. (utilizados para análises auxiliares)

**Observação:** A SWAPI retorna alguns campos como strings e pode haver valores como `"unknown"`; o pipeline converte essas entradas em `NaN`/`null` e realiza *casting* para tipos numéricos quando aplicável.

---

## 🧪 Metodologia (ETL + Análise)

1. **Extração (E)**
   - Requisições HTTP aos endpoints públicos (paginados).
   - Consolidação de páginas em um único *dataset* bruto.
2. **Transformação (T)**
   - Normalização de colunas.
   - Conversão do campo `population` para tipo numérico:
     - Valores `"unknown"` → `NaN`/nulo.
     - Remoção de separadores não numéricos, quando houver.
   - Remoção de duplicidades.
   - Seleção de colunas relevantes.
3. **Carga (L)**
   - Persistência do *dataset* limpo (ex.: `data/planets_clean.csv` ou `data/planets_clean.parquet`).
4. **Análise Descritiva**
   - Contagem de registros válidos, estatísticas (mín/máx/mediana/quartis) para `population`.
   - Listagem **Top 10** por `population` (descendente).
5. **Visualização**
   - Gráfico de barras com **os 10 planetas mais populosos**.
   - Tabela final com `name` e `population`.

---

## 🛠️ Stack Sugerida

- **Linguagem:** Python 3.11+
- **Bibliotecas:** `requests`, `pandas`, `matplotlib` (ou `plotly`)
- **Ambiente:** `venv` (ou `conda`/`poetry`)
- **Persistência:** CSV/Parquet em `data/`

---

## 🚀 Como Executar

O projeto foi desenvolvido em um notebook Jupyter (`starwars.ipynb`). Para executá-lo, basta ter um ambiente Python com as bibliotecas necessárias (como Pandas e Matplotlib) instalado e abrir o arquivo.

---

## 📊 Resultado Esperado

- **Gráfico:** barras com os 10 planetas mais populosos (eixo X: nomes; eixo Y: população).
- **Tabela final:** duas colunas — name e population — com os mesmos 10 planetas ordenados.
> Nota: Como a SWAPI pode retornar "unknown" para population, apenas planetas com valor numérico válido entram no ranking.

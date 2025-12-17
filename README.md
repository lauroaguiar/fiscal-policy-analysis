# 📊 Conjuntura Macroeconômica 2025.1: Seção Fiscal

> **Repositório oficial da análise fiscal desenvolvida para o relatório de Conjuntura Macroeconômica.**

[![R](https://img.shields.io/badge/Made_with-R-blue?style=for-the-badge&logo=R)](https://www.r-project.org/)
[![Data Source](https://img.shields.io/badge/Data-IMF%20%26%20World%20Bank-orange?style=for-the-badge)](https://www.imf.org/en/Data)
[![Status](https://img.shields.io/badge/Status-Concluído-success?style=for-the-badge)]()

## 👥 Autores
* **João Abdo**
* **João Moreno**
* **Lauro Aguiar**

---

## 🎯 Objetivo do Projeto

Este projeto tem como foco a análise da **sustentabilidade fiscal** e da **eficiência do gasto público** no Brasil, comparando-o com pares regionais (América Latina) e blocos econômicos (BRICS e Países Desenvolvidos). 

A análise foge do lugar comum ao não olhar apenas para o *quanto* se gasta, mas para a *qualidade* desse gasto, construindo indicadores próprios a partir de microdados.

---

## 🛠 Metodologia e Abordagem Técnica

A seção fiscal foi construída utilizando uma abordagem orientada a dados (*data-driven*), automatizando a coleta e o tratamento de grandes bases de dados internacionais.

### 1. Coleta Automatizada de Dados (APIs)
Em vez de baixar planilhas estáticas, desenvolvemos scripts em **R** para conectar diretamente às APIs de instituições multilaterais (Os dados do WBStats e GMD não foram utilizados na análise de conjuntura, mas sim os gráficos feitos pelo Itáu).
* **FMI (IMF DataMapper API):** Para dados macrofiscais (Dívida Bruta, Resultado Primário, Receitas e Despesas) de países da América Latina (`BRA`, `ARG`, `CHL`, `COL`, `PRY`, `PER`, `MEX`, `URY`).
* **Banco Mundial (WBStats):** Para indicadores socioeconômicos utilizados no cálculo de eficiência.
* **Global Macro Database (GMD):** Para séries históricas longas e comparações estruturais.

### 2. Índice de Eficiência do Gasto Público (Custom Index)
Um dos diferenciais deste trabalho foi a criação de um **Índice de Qualidade dos Bens Públicos**. Utilizamos a biblioteca `wbstats` para agregar indicadores em 5 dimensões:

* 📚 **Educação:** Alfabetização, PISA e conclusão do ensino secundário.
* 🏥 **Saúde:** Expectativa de vida e mortalidade neonatal.
* ⚖️ **Administração:** Controle de corrupção, qualidade judicial e burocracia.
* 🤝 **Equidade:** Participação na renda dos 40% mais pobres.
* ⚡ **Infraestrutura:** Acesso à eletricidade e segurança pública.

> **Fórmula da Eficiência:**
> $$ \text{Eficiência} = \frac{\text{Índice de Qualidade dos Bens Públicos}}{\text{Gasto Público (% PIB)}} $$

---

## 📈 Principais Resultados (Highlights)

O código gera visualizações que respondem às seguintes perguntas:
1.  **Sustentabilidade:** A trajetória da Dívida Bruta do Brasil é explosiva comparada aos pares da LATAM?
2.  **Resultado Fiscal:** Como o *Net Lending/Borrowing* do Brasil se comporta frente à volatilidade regional?
3.  **Custo-Benefício:** O Brasil gasta muito? E esse gasto se traduz em bens públicos de qualidade comparável aos países da OCDE ou BRICS?

---

## 💻 Estrutura do Código

Abaixo, um exemplo simplificado de como estruturamos a extração de dados do FMI para garantir reprodutibilidade:

```r
# Exemplo de extração via API do FMI utilizada no projeto
fetch_indicator <- function(indicator_id) {
  base_url <- "[https://www.imf.org/external/datamapper/api/v1](https://www.imf.org/external/datamapper/api/v1)"
  url <- sprintf("%s/%s/%s?periods=%s", base_url, indicator_id, paste(paises, collapse = "/"), periods_param)
  
  resp <- GET(url)
  # ... (Processamento e limpeza do JSON) ...
  return(data_indicator)
}
```

## 📦 Pacotes Utilizados

A análise depende de um conjunto robusto de bibliotecas do R:

* **Manipulação de Dados:** `tidyverse`, `dplyr`, `janitor`, `lubridate`
* **Econometria e Séries Temporais:** `urca`, `vars`, `forecast`, `tseries`, `mFilter`
* **Dados Financeiros/Macro:** `GetBCBData`, `wbstats`, `globalmacrodata`, `imf.data`
* **Visualização:** `ggplot2`, `plotly`, `gridExtra`, `scales`

---

## 🚀 Como Executar

1.  Clone este repositório.
2.  Abra o arquivo principal do projeto no RStudio.
3.  Certifique-se de que todas as dependências estão instaladas (o script possui uma função `install_if_missing` automática).
4.  Execute os chunks para baixar os dados mais recentes e gerar os gráficos.

---
*Este projeto é de cunho acadêmico e educacional, desenvolvido no âmbito do [IbMacro]([url](https://br.linkedin.com/company/ibmacro))..*

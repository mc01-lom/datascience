
---

## Sumário

1. [Análise de Tendências](#2-análise-de-tendências)
2. [Análise por Fornecedor](#3-análise-por-fornecedor)
3. [Análise por Categoria](#4-análise-por-categoria)
4. [Pareto](#5-pareto)
5. [Com / Sem Contrato — Maverick Spend](#6-com--sem-contrato--maverick-spend)
6. [Produto / Serviço](#7-produto--serviço)

---

## 2. Análise de Tendências

> **Objetivo:** Compreender a evolução temporal do spend, identificar sazonalidades, tendências de crescimento e anomalias no comportamento de gasto ao longo do tempo (2022–2026).

| Pergunta de Negócio | Indicador / Métrica | Visão / Gráfico |
|---|---|---|
| O spend está crescendo, estável ou caindo? | Spend total por período · Variação YoY (%) | Linha temporal mensal + barras anuais com % de variação |
| Existe sazonalidade no gasto do banco? | Spend médio por mês (agregado multi-ano) | Linha de sazonalidade (Jan–Dez) |
| Quais categorias estão crescendo ou encolhendo mais rápido? | Variação YoY por categoria N1 | Linhas múltiplas por categoria ou heatmap de variação |
| O crescimento é orgânico (mais transações) ou de preço (ticket maior)? | Decomposição: Δ Volume vs. Δ Ticket Médio | Barras empilhadas ou waterfall de decomposição |
| Há tendência de concentração temporal (picos de fim de ano/trimestre)? | Spend por trimestre · % do ano concentrado no Q4 | Barras por trimestre + indicador de concentração temporal |
| O ritmo de novos fornecedores está acelerando? | Nº de fornecedores com 1ª transação por período | Linha de novos fornecedores/mês *(crítico: investigar salto +90% em 2025)* |

### Notas e Referências
- Benchmark Aberdeen Group: spend estável a crescente é esperado em programas maduros
- O salto de fornecedores em 2025 (6.130 → 11.694, +90,8%) deve ser investigado nesta análise como anomalia
- Variação YoY de spend total: banda esperada de ±10% em anos sem eventos extraordinários

---

## 3. Análise por Fornecedor

> **Objetivo:** Mapear o universo de fornecedores do banco, identificar dependências, riscos de concentração, e perfis de relacionamento (volume, valor, atividade).

| Pergunta de Negócio | Indicador / Métrica | Visão / Gráfico |
|---|---|---|
| Quem são os maiores fornecedores do banco? | Ranking por spend total | Tabela ou barras top N fornecedores |
| Qual a dependência de poucos fornecedores? | % spend nos top 5 / 10 / 20 | Cards de concentração + curva de Pareto |
| O risco de concentração está dentro do aceitável? | HHI por fornecedor (global e por categoria) | Card HHI + classificação DOJ (< 1.000 / 1.000–1.800 / > 1.800) |
| Existem fornecedores com volume crescente fora do radar? | Variação YoY de spend por fornecedor | Tabela de "fornecedores em ascensão" |
| Há fornecedores ativos em múltiplas categorias? | Nº de categorias N1 distintas por fornecedor | Tabela ou scatter fornecedor × nº categorias |
| Qual o relacionamento volume × ticket médio por fornecedor? | Spend total vs. nº transações vs. ticket médio | Scatter / gráfico de bolhas |
| Quantos fornecedores são ativos vs. inativos? | Flag `flag_ativo` (sem transação nos últimos 12 meses) | Card de ativos/inativos + lista para limpeza de cadastro |

### Notas e Referências
- HHI: Hirschman (1945) e Herfindahl (1950) — método de somar quadrados de market shares
- Classificação DOJ: HHI < 1.000 = não concentrado · 1.000–1.800 = moderado · > 1.800 = altamente concentrado
- Benchmark McKinsey Spendscape: caso bancário europeu com 1M+ line items e 10% de consolidação de fornecedores

---

## 4. Análise por Categoria

> **Objetivo:** Compreender a estrutura de gastos por tipo de compra (taxonomia UNSPSC adaptada, 4 níveis), identificar categorias críticas, mal classificadas ou com risco de fornecimento.

| Pergunta de Negócio | Indicador / Métrica | Visão / Gráfico |
|---|---|---|
| Onde está concentrado o gasto por tipo de compra? | Spend por N1 / N2 / N3 / N4 | Treemap hierárquico com drill-down |
| Quais categorias têm maior risco de concentração de fornecedores? | HHI por categoria N1 | Barras de HHI por N1, ordenado decrescente |
| Qual categoria tem maior % fora de contrato? | Maverick spend (%) por categoria | Barras horizontais com linha de meta (10% / 5%) |
| Existem categorias mal classificadas? | % spend em "Outros / Não Classificado" | Card com alerta se acima da meta (> 5%) |
| Como cada categoria evolui no tempo? | Spend por categoria × mês | Heatmap categoria × mês |
| Qual categoria tem maior fragmentação de fornecedores? | Nº fornecedores distintos por categoria | Barras + cruzamento com HHI |
| Existem categorias de fornecedor único (risco de fornecimento)? | Single-source categories (1 único fornecedor por categoria N2/N3) | Lista / contagem com % do spend afetado |

### Notas e Referências
- Taxonomia: UNSPSC v26 adaptado + categorias existentes no banco (Ariba)
- 12 segmentos N1: Tecnologia · Serviços Profissionais · Facilities e MDO · Call Center e BPO · Logística e Transporte · Marketing e Comunicação · Benefícios e RH · Seguros · Materiais e Suprimentos · Viagens e Hospedagem · Gráfica e Impressão · Outros / Não Classificado
- Regra de ouro Sievo: o nível N4 deve ser granular o suficiente para um único RFP
- Meta de cobertura: < 5% em "Outros / Não Classificado" (KPI de qualidade de dado)

---

## 5. Pareto

> **Objetivo:** Aplicar o princípio de Pareto (80/20) ao spend para identificar quais fornecedores e categorias merecem atenção estratégica prioritária, definir classificação ABC e monitorar evolução da concentração.

| Pergunta de Negócio | Indicador / Métrica | Visão / Gráfico |
|---|---|---|
| Quantos fornecedores concentram 80% do spend? | % fornecedores que somam 80% do valor total | Curva de Pareto (barras + linha % acumulado + referência 80%) |
| O mesmo princípio vale para categorias? | % categorias N2/N3 que somam 80% do spend | Curva de Pareto por categoria |
| A concentração está piorando ou melhorando no tempo? | Nº de fornecedores no "top 80%" por ano | Linha temporal do tamanho do grupo Pareto |
| Qual o ponto de corte ideal para priorização estratégica? | Classificação ABC (A = top 80% · B = próximos 15% · C = últimos 5%) | Tabela com classificação e cores por faixa |
| A curva de Pareto está "normal" comparada a benchmarks de mercado? | Inclinação da curva vs. referência de mercado | Anotação no gráfico com benchmark quando disponível |

### Notas e Referências
- Referência: Pandit & Marmanis (2008) — spend analysis começa pela identificação dos fornecedores críticos
- Aberdeen Group (Limberakis, 2011): organizações Best-in-Class usam Pareto como ponto de partida para sourcing estratégico
- Classificação ABC é a base para definir quais categorias entram em processo formal de RFP/negociação

---

## 6. Com / Sem Contrato — Maverick Spend

> **Objetivo:** Medir e monitorar o quanto do spend está coberto por contratos vigentes, identificar onde e por quem o gasto fora de política ocorre, e apoiar ações de regularização e controle.

| Pergunta de Negócio | Indicador / Métrica | Visão / Gráfico |
|---|---|---|
| Qual % do gasto total está coberto por contrato vigente? | Contract Coverage (%) = Spend com contrato / Spend total | Gauge / velocímetro com meta > 80% |
| Onde está concentrado o gasto sem contrato? | Maverick spend (R$) por categoria / área / fornecedor | Barras horizontais — top ofensores |
| O maverick spend está aumentando ou diminuindo? | Evolução mensal do % maverick | Linha temporal com banda de meta |
| Existem contratos prestes a vencer que vão gerar maverick? | Contratos com vencimento em 90 / 180 dias | Tabela de alertas de vencimento |
| Quais áreas requisitantes mais geram compras sem contrato? | Maverick spend por `dim_area` (diretoria / superintendência) | Barras por estrutura organizacional |
| O maverick spend é concentrado em poucos fornecedores ou disperso? | Nº de fornecedores únicos no maverick + % do valor | Card + cruzamento com Pareto do maverick |

### Notas e Referências
- Meta: Contract Coverage > 80% · Maverick Spend < 10% (Best-in-class: < 5%) — Aberdeen Group (Limberakis, 2011)
- KYS (Know Your Supplier): spend com fornecedores KYS aprovado deve ser > 95%
- Esteiras de gasto do banco: Contratual · Pedido sem Contrato · Baixo Valor · Mercado IGA · Extra Compras · Fora da Política
- GAO-04-870: compliance de contratos é um dos pilares centrais do spend analysis em organizações maduras

---

## 7. Produto / Serviço

> **Objetivo:** Analisar o spend pela natureza do que está sendo adquirido (produto vs. serviço, tipo de despesa), identificar tail spend por natureza, inconsistências de classificação e oportunidades de consolidação.

| Pergunta de Negócio | Indicador / Métrica | Visão / Gráfico |
|---|---|---|
| Qual a natureza de pagamento mais relevante em valor? | Spend por `descricao_natureza` | Barras horizontais ordenadas por valor |
| Como a natureza se relaciona com a categoria (são consistentes)? | Cruzamento natureza de pagamento × categoria N1 | Heatmap ou matriz de consistência |
| Existe gasto disperso e pulverizado por tipo de produto/serviço? | % tail spend por natureza (fornecedores < R$100K/ano) | Barras + lista de candidatos à consolidação |
| Qual o ticket médio típico por natureza de pagamento? | Valor médio e mediano por `descricao_natureza` | Box plot em escala log10 por natureza |
| Há naturezas de pagamento mal definidas ou genéricas demais? | % spend em "Outros Serviços" por natureza | Card de qualidade de dado |
| A distribuição de valores por natureza é homogênea ou tem outliers? | Distribuição de valores em escala log10 | Histograma com curva normal + box plot por natureza |

### Notas e Referências
- `dim_natureza_pagamento`: campo existente nas bases do banco, serve como ponto de partida para a taxonomia
- Campo `macro_natureza` será criado por ML (agrupamento de naturezas similares)
- Tail spend threshold: fornecedores com gasto < R$100K/ano por categoria
- Referência: Coupa Tail Spend Guide (2026) — AI aumenta visibilidade em 24,4% e savings em 8,1% no tail spend
- Referência: Ivalua (2026) — metodologia de tail spend: empresas podem realizar 5–20% de savings via consolidação

---

## Visão Consolidada dos KPIs por Análise

| Análise | KPI Principal | Meta / Benchmark | Fonte |
|---|---|---|---|
| Tendências | Variação YoY do spend | Banda ±10% em anos normais | Aberdeen Group |
| Fornecedor | HHI global | < 1.000 (não concentrado) | U.S. DOJ |
| Categoria | % Spend "Não Classificado" | < 5% | KPI interno |
| Pareto | Nº fornecedores no top 80% | Mapear e monitorar | Pandit & Marmanis |
| Com/Sem Contrato | Contract Coverage | > 80% | Aberdeen Group |
| Com/Sem Contrato | Maverick Spend | < 10% (best-in-class: 5%) | Aberdeen Group |
| Produto/Serviço | % Tail Spend | Mapear e reduzir | Coupa / Ivalua |

---

## Referências Utilizadas

| Referência | Contribuição |
|---|---|
| Pandit & Marmanis (2008) | Framework metodológico fundacional |
| Aberdeen Group — Limberakis (2011) | Benchmarks e metas (Contract Coverage, Maverick, SUM) |
| U.S. GAO-04-870 (2004) | Best practices em compliance e governança |
| U.S. DOJ — HHI | Faixas de concentração (< 1.000 / 1.000–1.800 / > 1.800) |
| McKinsey Spendscape | Casos práticos em serviços financeiros |
| Sievo — Spend Categorization | Regra de ouro do N4 · 94–98% UNSPSC accuracy |
| Coupa Tail Spend Guide (2026) | Tail spend: +24,4% visibilidade · +8,1% savings |
| Ivalua (2026) | Tail spend: 5–20% savings via consolidação |
| UNSPSC v26 — UNDP | Taxonomia oficial (158.448 códigos) |


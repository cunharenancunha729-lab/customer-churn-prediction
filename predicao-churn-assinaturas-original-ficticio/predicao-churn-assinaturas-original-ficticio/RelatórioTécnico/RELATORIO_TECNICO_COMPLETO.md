# Relatório Técnico — Sistema de Predição de Cancelamento de Assinaturas

**Projeto:** Sistema Inteligente de Predição de Cancelamento (Churn)
**Base de dados:** Streaming Data Science — 450 clientes, 54 variáveis
**Autor:** Renan Cunha

---

## 1. Visão geral da base de dados

O dataset contém **450 clientes** de uma plataforma de streaming, com **54 variáveis** (demográficas, comportamentais, financeiras e de engajamento).

Quanto à situação atual da conta, os clientes se dividem em três status:

| Status | Clientes | % da base |
|---|---|---|
| Ativo | 270 | 60% |
| Cancelado (Inativo) | 90 | 20% |
| Inadimplente | 90 | 20% |

> **Nota sobre metodologia:** o modelo de Machine Learning foi treinado para identificar tanto clientes **cancelados** quanto **inadimplentes** como "risco/churn" (180 clientes, 40% da base), já que ambos representam perda de receita ativa. Já a análise de **motivos de cancelamento** (seção 2) considera apenas os 90 clientes que efetivamente cancelaram, pois são os únicos com motivo registrado no sistema.

## 2. Clientes cancelados e motivos

**90 clientes (20% da base) cancelaram efetivamente a assinatura.** Os motivos registrados:

| Motivo | Clientes | % dos cancelamentos | Avaliação média dada à plataforma |
|---|---|---|---|
| Não usa mais | 19 | 21,1% | 2,42 |
| Preço alto | 14 | 15,6% | 3,07 |
| Migrou para concorrente | 13 | 14,4% | 2,38 |
| Pouco conteúdo | 12 | 13,3% | 2,67 |
| Problemas financeiros | 12 | 13,3% | 2,75 |
| Problemas técnicos | 11 | 12,2% | 2,36 |
| Falta de tempo | 9 | 10,0% | 3,11 |

**Insight real dos dados:** clientes que cancelaram por problemas técnicos, migração para concorrente ou "não usa mais" deram as notas mais baixas à plataforma (2,36–2,42) — sugerindo insatisfação real com o produto. Já quem cancelou por preço alto ou falta de tempo avaliou melhor a plataforma (3,07–3,11), indicando que a saída foi por motivos externos, não por insatisfação com o serviço em si.

## 3. Modelos de Machine Learning — comparação

Foram treinados dois classificadores para prever o risco (cancelado + inadimplente vs. ativo):

| Modelo | Acurácia | Precisão (risco) | Recall (risco) | F1-Score (risco) |
|---|---|---|---|---|
| **Regressão Logística** | **93,33%** | 89% | **94%** | 92% |
| Árvore de Decisão | 90,00% | 89% | 86% | 87% |

### Matriz de confusão (conjunto de teste, 90 clientes)

**Regressão Logística**

|  | Previsto: Sem risco | Previsto: Risco |
|---|---|---|
| **Real: Sem risco** | 50 | 4 |
| **Real: Risco** | 2 | 34 |

**Árvore de Decisão**

|  | Previsto: Sem risco | Previsto: Risco |
|---|---|---|
| **Real: Sem risco** | 50 | 4 |
| **Real: Risco** | 5 | 31 |

**Modelo escolhido: Regressão Logística.** Apesar da acurácia próxima entre os dois, ela identificou corretamente 34 dos 36 clientes em risco no teste (recall de 94%), deixando passar apenas 2 — o melhor desempenho na métrica mais importante para esse tipo de problema.

## 4. Previsão sobre a base ativa

Aplicando o modelo treinado sobre os **270 clientes atualmente ativos** (nunca cancelaram nem estão inadimplentes), o modelo sinalizou:

**4 clientes (1,5% da base ativa) com alto risco de cancelamento.**

Esses clientes têm em comum: avaliação média da plataforma mais baixa (2,50 vs. 2,97 dos demais ativos) e tempo de casa bem menor (16,75 meses vs. 31 meses de média dos demais) — um padrão consistente com o perfil de quem já cancelou por insatisfação.

> Esse número é propositalmente conservador (usa o limiar padrão de 50% de probabilidade do modelo). Ele reflete apenas clientes com risco já muito próximo do padrão histórico de quem cancelou — não é uma estimativa de "todo mundo que pode vir a cancelar algum dia".

## 5. Impacto na receita

**Cancelamentos já realizados (90 clientes "Inativo"):**
- Receita mensal recorrente perdida: **R$ 3.091,00/mês**
- Projeção anual: **R$ 37.092,00/ano**

**Clientes inadimplentes (90 clientes, receita em risco imediato):**
- Receita mensal exposta: **R$ 3.421,00/mês**

**Clientes ativos sinalizados como risco pelo modelo (4 clientes):**
- Receita mensal em risco: **R$ 154,60/mês**
- Projeção anual: **R$ 1.855,20/ano**

## 6. Plano de ação recomendado (com base nos dados)

| Frente | Ação | Baseado em |
|---|---|---|
| **Insatisfação com produto** | Investigar problemas técnicos relatados e acompanhar de perto clientes com avaliação ≤ 2 — são o grupo com maior taxa de cancelamento por insatisfação real | Notas médias de 2,36–2,42 nos motivos "problemas técnicos", "migrou" e "não usa mais" |
| **Sensibilidade a preço** | Oferecer downgrade guiado ou desconto para clientes de planos mais caros com baixo uso, antes que cancelem | "Preço alto" é o 2º motivo mais citado (15,6%) |
| **Inadimplência** | Régua de cobrança proativa (lembretes antes do vencimento) para os 90 clientes inadimplentes — grupo do mesmo tamanho dos cancelados, com receita similar em risco | R$ 3.421/mês em receita exposta |
| **Retenção preditiva** | Acompanhamento prioritário dos 4 clientes ativos sinalizados pelo modelo, com contato de relacionamento antes que o padrão de queda de avaliação se repita | Avaliação e tempo de casa abaixo da média entre os sinalizados |
| **Engajamento** | Campanhas de reativação para clientes com poucos perfis criados em relação às telas contratadas (indício de plano superdimensionado) | Padrão observado nos cancelamentos por "pouco conteúdo" e "não usa mais" |

## 7. Limitações

- O modelo foi avaliado em uma base de teste pequena (90 clientes) — os percentuais tendem a variar com mais dados
- Apenas 4 clientes ativos foram sinalizados com o limiar padrão (50%); um limiar mais sensível aumentaria a lista de alerta, mas também aumentaria falsos positivos
- Não foi feita validação cruzada (k-fold) nesta versão, o que ajudaria a confirmar a estabilidade das métricas

---

*Relatório gerado a partir da execução real do pipeline do notebook sobre o dataset completo (450 clientes).*


 # 📉 Previsão de Churn de Clientes

Projeto de Ciência de Dados e Machine Learning para prever o cancelamento (churn) de clientes de um serviço de assinaturas, comparando diferentes modelos de classificação.

## 📌 Sobre o projeto

Empresas de assinatura perdem receita quando clientes cancelam sem aviso. Este projeto treina modelos capazes de identificar, com antecedência, quais clientes têm maior risco de churn — permitindo ações de retenção direcionadas.

- **Dataset**: 450 clientes, 54 variáveis (sintético)
- **Problema**: classificação binária (churn / não churn)

## 📊 Resultados

| Modelo | Acurácia | Recall (churn) |
|---|---|---|
| **Regressão Logística** | **93,33%** | **94%** |
| Árvore de Decisão | 90% | — |

A Regressão Logística foi o modelo escolhido: além da maior acurácia, teve recall de 94% para a classe de churn — ou seja, identifica corretamente a grande maioria dos clientes que de fato cancelariam, que é a métrica mais importante nesse tipo de problema (o custo de não identificar um churn é maior que o de um falso positivo).

## 🛠️ Tecnologias

Python · Pandas · NumPy · Matplotlib · Seaborn · Scikit-learn

## 🔍 Etapas do projeto

1. Tratamento e limpeza dos dados
2. Análise exploratória (EDA)
3. Treinamento e comparação de modelos (Regressão Logística vs. Árvore de Decisão)
4. Avaliação com métricas de classificação (acurácia, recall, matriz de confusão)

## ▶️ Como rodar

```bash
git clone https://github.com/cunharenancunha729-lab/customer-churn-prediction.git
cd customer-churn-prediction
pip install -r requirements.txt
jupyter notebook
```

---

📫 Desenvolvido por [Renan Cunha](https://github.com/cunharenancunha729-lab)

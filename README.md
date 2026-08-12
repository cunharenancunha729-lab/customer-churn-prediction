 Customer Churn Prediction
Sistema Inteligente de Predição de Cancelamento de Assinaturas

Projeto de Ciência de Dados e Machine Learning desenvolvido para analisar o comportamento de clientes de uma plataforma de streaming e identificar padrões relacionados ao cancelamento de assinaturas (Customer Churn).

O projeto apresenta um pipeline completo, desde a exploração e tratamento dos dados até a construção, avaliação e comparação de modelos de Machine Learning.

 Importante: todos os dados utilizados neste projeto são fictícios/sintéticos, criados exclusivamente para fins educacionais e de portfólio. Não são dados reais de clientes.

 Objetivo

O objetivo do projeto é utilizar dados de clientes para desenvolver uma solução preditiva capaz de identificar padrões associados ao cancelamento de assinaturas.

A proposta simula um cenário de negócio no qual uma empresa de streaming deseja utilizar Ciência de Dados e Inteligência Artificial para apoiar estratégias de retenção de clientes.

O projeto busca demonstrar, na prática, conhecimentos em:

Python para Ciência de Dados
Análise Exploratória de Dados
Limpeza e tratamento de dados
Engenharia de atributos
Transformação de variáveis categóricas
Machine Learning
Classificação
Avaliação de modelos
Interpretação de resultados
Análise orientada a problemas de negócio
 Problema de negócio

Em serviços baseados em assinatura, a perda de clientes representa um importante desafio.

A análise de Churn permite investigar:

Quais características e comportamentos estão associados ao cancelamento de uma assinatura?

A partir dessa pergunta, o projeto utiliza dados de clientes para construir modelos capazes de classificar o comportamento relacionado ao cancelamento.

A ideia é transformar dados históricos em informações que possam apoiar ações como:

Identificação de clientes com maior risco;
Estratégias de retenção;
Melhoria da experiência do cliente;
Análise de preços e planos;
Identificação de problemas recorrentes;
Tomada de decisão orientada por dados.
 Pipeline do projeto
Dados dos clientes
        ↓
Exploração dos dados
        ↓
Análise da estrutura
        ↓
Tratamento de valores ausentes
        ↓
Verificação de duplicidades
        ↓
Análise exploratória
        ↓
Transformação das variáveis
        ↓
One-Hot Encoding
        ↓
Definição da variável alvo
        ↓
Seleção das features
        ↓
Divisão treino / teste
        ↓
Machine Learning
        ↓
Regressão Logística
        ↓
Árvore de Decisão
        ↓
Avaliação dos modelos
        ↓
Análise dos motivos de cancelamento
Dataset

O dataset utilizado contém:

450 clientes
54 variáveis
Informações demográficas
Informações financeiras
Dados relacionados à assinatura
Informações de pagamento
Dados de utilização da plataforma
Avaliação da plataforma
Status da assinatura
Motivos de cancelamento

Entre as variáveis analisadas estão:

Idade
Gênero
Estado civil
Profissão
Faixa de renda
Plano de assinatura
Valor do plano
Ciclo de faturamento
Status
Dias de atraso
Tempo como cliente
Valor total pago
Quantidade de perfis
Quantidade de telas contratadas
Dispositivo principal
Idioma preferido
Avaliação da plataforma
Motivo de cancelamento
Dados fictícios

O dataset foi criado para representar um cenário semelhante ao encontrado em empresas de serviços por assinatura.

Nenhuma informação representa clientes reais.

 Tratamento dos dados

Inicialmente foi realizada uma análise da qualidade dos dados para identificar valores ausentes e possíveis duplicidades.

Foram analisados campos relacionados a:

Telefone fixo
Código de indicação
Cupom de desconto
Dados de cartão
Validade do cartão
E-mail alternativo
Complemento do endereço
Entre outros.

Os valores ausentes foram tratados utilizando estratégias como:

Moda para variáveis categóricas;
Mediana para variável numérica selecionada.

Também foi realizada uma verificação de registros duplicados.

Resultado:

Registros duplicados encontrados: 0
 Análise Exploratória de Dados

A análise exploratória buscou compreender o perfil dos clientes e encontrar padrões relevantes antes da aplicação dos modelos.

Foram realizadas análises e visualizações envolvendo:

Distribuição de idade

Análise da distribuição etária dos clientes da plataforma.

Faixa de renda

Análise da quantidade de clientes em diferentes faixas de renda.

Relação entre renda e valor pago

Foi calculada a média do valor total pago por faixa de renda para compreender diferenças de comportamento financeiro.

Motivos de cancelamento

Também foi realizada uma análise específica dos principais motivos associados ao cancelamento.

 Principais motivos de cancelamento

Entre os motivos identificados no dataset estão:

Motivo	Clientes
Não usa mais	19
Preço alto	14
Migrou para concorrente	13
Problemas financeiros	12
Pouco conteúdo	12
Problemas técnicos	11
Falta de tempo	9

A análise também relacionou os motivos de cancelamento com a avaliação atribuída pelos clientes à plataforma.

Isso permite ir além da previsão e investigar por que os clientes estão cancelando.

🤖 Machine Learning

Após a preparação dos dados, foi construída a variável alvo relacionada ao Churn.

As variáveis categóricas foram transformadas utilizando One-Hot Encoding.

Após o processo de transformação:

Dataset original:
450 registros × 54 variáveis

Após One-Hot Encoding:
450 registros × 5.037 variáveis

Features utilizadas na modelagem:
450 registros × 416 features

Variáveis identificadoras, informações diretamente relacionadas ao alvo e campos com potencial de data leakage foram removidos das features utilizadas na modelagem.

 Divisão dos dados

Os dados foram divididos em:

80% → Treinamento
20% → Teste

Foi utilizado:

random_state = 42

O conjunto de teste utilizado na avaliação possui:

90 registros
 Modelos utilizados

Foram comparados dois algoritmos de classificação.

1. Regressão Logística

A Regressão Logística foi utilizada como modelo de classificação para prever o comportamento relacionado ao cancelamento.

O modelo apresentou:

Acurácia: 93,33%
Precision — classe de cancelamento: 89%
Recall — classe de cancelamento: 94%
F1-score — classe de cancelamento: 92%
2. Árvore de Decisão

A Árvore de Decisão foi utilizada como segundo modelo para comparação.

Resultados:

Acurácia: 90%
Precision — classe de cancelamento: 89%
Recall — classe de cancelamento: 86%
F1-score — classe de cancelamento: 87%
 Comparação dos modelos
Modelo	Acurácia	Precision Churn	Recall Churn	F1-score Churn
Regressão Logística	93,33%	89%	94%	92%
Árvore de Decisão	90%	89%	86%	87%
Resultado

A Regressão Logística apresentou o melhor desempenho no experimento, alcançando aproximadamente 93,3% de acurácia no conjunto de teste.

Além disso, apresentou 94% de recall para a classe de cancelamento, indicando uma boa capacidade de identificar os clientes classificados como churn no conjunto avaliado.

 Insights de negócio

Além da construção dos modelos, o projeto também buscou entender os fatores relacionados ao cancelamento.

Os principais motivos encontrados foram:

1. Falta de utilização

O motivo mais frequente foi:

"Não usa mais"

Isso indica uma oportunidade de investigar engajamento e utilização da plataforma.

2. Preço

O segundo maior motivo foi:

"Preço alto"

Esse resultado pode apoiar análises relacionadas a planos, preços, descontos e percepção de custo-benefício.

3. Concorrência

Também foi identificado um número relevante de clientes que:

Migraram para concorrentes.

Esse comportamento pode indicar a necessidade de analisar diferenciais competitivos e experiência oferecida pela plataforma.

4. Problemas financeiros

Outro grupo relevante está relacionado a dificuldades financeiras.

Isso pode ser utilizado em futuras análises de retenção e estratégias de cobrança.

5. Problemas técnicos e conteúdo

Também foram identificados cancelamentos relacionados a:

Problemas técnicos;
Pouco conteúdo;
Falta de tempo.

Esses fatores podem orientar futuras ações de produto e experiência do usuário.

 🛠️ Tecnologias utilizadas
Linguagem
Python
Bibliotecas
Pandas
NumPy
Matplotlib
Seaborn
Scikit-learn
Machine Learning
Regressão Logística
Árvore de Decisão
One-Hot Encoding
Train/Test Split
Avaliação
Accuracy
Precision
Recall
F1-score
Classification Report
Ambiente
Jupyter Notebook
Este projeto demonstra a capacidade de desenvolver um fluxo de Ciência de Dados de ponta a ponta, incluindo:

Problema de negócio
        ↓
Coleta / Dataset
        ↓
Tratamento
        ↓
EDA
        ↓
Feature Engineering
        ↓
Machine Learning
        ↓
Avaliação
        ↓
Comparação
        ↓
Insights
        ↓
Aplicação no negócio

Mais do que simplesmente treinar um modelo, o projeto busca conectar dados, Machine Learning e tomada de decisão.

 Possíveis evoluções

Como próximos passos para uma versão mais avançada, o projeto poderia incluir:

Validação cruzada;
Otimização de hiperparâmetros;
Random Forest;
Gradient Boosting;
XGBoost;
Análise de importância das variáveis;
Matriz de confusão;
Curva ROC e AUC;
Ajuste de threshold;
Pipeline de Machine Learning;
API para disponibilização do modelo;
Sistema de classificação de novos clientes;
Monitoramento do desempenho do modelo.


 Objetivo profissional

Este projeto faz parte do meu portfólio de desenvolvimento em:

Ciência de Dados | Machine Learning | Inteligência Artificial | Python | Análise de Dados

O objetivo é desenvolver soluções que utilizem dados e inteligência artificial para resolver problemas de negócio, combinando análise, programação e modelos preditivos.

 Autor
Renan Henrique Martins Cunha

Estudante de Análise e Desenvolvimento de Sistemas e Técnico em Inteligência Artificial, com foco em:

Ciência de Dados
Machine Learning
Inteligência Artificial
Python
Análise de Dados
Desenvolvimento de soluções orientadas por dados
🔗 Conecte-se comigo

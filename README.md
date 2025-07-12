# 📊 Telecom X: Previsão de Evasão de Clientes (Churn Prediction)

## Visão Geral do Projeto
Este projeto de Ciência de Dados tem como objetivo principal desenvolver modelos preditivos para identificar clientes com alta probabilidade de evasão (churn) na empresa de telecomunicações "Telecom X". A retenção de clientes é um pilar estratégico para qualquer negócio, e a capacidade de prever o churn permite que a empresa atue proativamente, implementando estratégias de fidelização e minimizando perdas financeiras.

Neste repositório, você encontrará um pipeline completo de Machine Learning, desde o pré-processamento robusto dos dados até a avaliação de modelos e a extração de insights acionáveis para o negócio.

## 🎯 Objetivos do Desafio
Preparação de Dados: Realizar limpeza, transformação, engenharia de features e codificação de variáveis para adequação aos modelos de ML.

Análise Exploratória de Dados (EDA): Entender a distribuição dos dados e as relações entre as variáveis, com foco especial na variável alvo (churn).

Balanceamento de Classes: Tratar o desequilíbrio entre as classes de churn (clientes que evadiram vs. clientes que permaneceram) para evitar viés nos modelos.

Modelagem Preditiva: Treinar e comparar múltiplos modelos de classificação para prever o churn.

Avaliação de Modelos: Utilizar métricas de desempenho relevantes (Acurácia, Precisão, Recall, F1-score, Matriz de Confusão) para selecionar o modelo mais eficaz para o problema de negócio.

Interpretabilidade: Analisar a importância das variáveis para entender os principais fatores que impulsionam a evasão.

Conclusões Estratégicas: Fornecer recomendações baseadas em dados para a Telecom X, visando a retenção de clientes.

## 📁 Estrutura do Repositório
TelecomX_Data.json: Dados brutos da Telecom X (fonte original).

telecomX_datos.csv: Base de dados pré-processada e tratada, pronta para a modelagem (gerada pela Parte 1 do Colab).

TelecomX_Customer_Retention_Study.ipynb: Notebook/script da Parte 1, responsável pelo carregamento, limpeza e pré-processamento dos dados, salvando o resultado em telecomX_datos.csv.

TelecomX_Previsao-de-Evasao-de-Clientes.ipynb: Notebook/script da Parte 2, que carrega os dados processados e executa as etapas de modelagem, avaliação e análise de importância de variáveis.

## 🚀 Metodologia
O projeto seguiu as seguintes etapas:

Carregamento e Pré-processamento de Dados:

Dados brutos carregados de um arquivo JSON.

Colunas aninhadas foram "achatadas" para facilitar a manipulação.

Renomeação de colunas para maior clareza e padronização.

Tratamento de valores duplicados e ausentes (especialmente na coluna total_charges).

Criação de uma nova feature: daily_charges (custo diário médio do cliente).

Binarização da variável churn_original para churn_bin (0=Ficou, 1=Evadiu) e outras colunas binárias.

Codificação de Variáveis Categóricas:

Utilização de pd.get_dummies para aplicar One-Hot Encoding nas variáveis categóricas (gender, internet_service, contract, payment_method). O parâmetro drop_first=True foi empregado para evitar multicolinearidade, garantindo a estabilidade e interpretabilidade dos modelos.

Balanceamento de Classes:

Identificado um desequilíbrio significativo na variável churn_bin (aproximadamente 73% de clientes que ficaram vs. 27% que evadiram).

Para mitigar o viés do modelo em favor da classe majoritária, aplicou-se a técnica de oversampling SMOTE (Synthetic Minority Over-sampling Technique), que gera amostras sintéticas da classe minoritária.

Normalização/Padronização de Dados:

StandardScaler foi aplicado para padronizar as features numéricas. Esta etapa é crucial para modelos sensíveis à escala (como a Regressão Logística), garantindo que todas as features contribuam igualmente para o treinamento do modelo e evitando a fuga de dados ao ser aplicada apenas nos dados de treino.

Análise de Correlação:

Uma matriz de correlação foi gerada para entender as relações lineares entre as variáveis preditoras e com a variável churn_bin. Gráficos de barras foram usados para visualizar as correlações mais fortes, e boxplots para explorar a relação de variáveis numéricas-chave com o churn.

Treinamento e Avaliação de Modelos:

Os dados foram divididos em conjuntos de treino (70%) e teste (30%) de forma estratificada para manter a proporção das classes.

Foram treinados dois modelos de classificação:

Regressão Logística: Um modelo linear, interpretável, treinado com dados padronizados.

Random Forest Classifier: Um modelo de ensemble baseado em árvores, robusto, capaz de capturar não-linearidades e menos sensível à escala dos dados (treinado com dados não padronizados).

Os modelos foram avaliados usando: Acurácia, Precisão, Recall, F1-score e Matriz de Confusão.

## 📈 Resultados e Insights Chave
Após a avaliação, o Random Forest Classifier demonstrou ser o modelo com melhor desempenho geral para este problema de previsão de evasão, especialmente no que tange ao Recall (capacidade de identificar corretamente clientes que irão evadir), uma métrica crítica para intervenções proativas.

Random Forest Metrics (Teste):

Acurácia: 0.8428

Precisão: 0.8298

Recall: 0.8625

F1-score: 0.8458

Regressão Logística Metrics (Teste):

Acurácia: 0.8228

Precisão: 0.8193

Recall: 0.8283

F1-score: 0.8238

A análise da importância das variáveis revelou os seguintes fatores-chave que influenciam a evasão:

tenure (Tempo de Contrato): A variável mais impactante. Clientes com menor tempo de contrato são significativamente mais propensos a evadir.

contract_Month-to-month (Contrato Mensal): Clientes com contratos mensais têm uma probabilidade muito maior de churn em comparação com contratos de um ou dois anos.

payment_method_Electronic check (Método de Pagamento Cheque Eletrônico): Este método de pagamento está fortemente associado a uma maior taxa de evasão.

internet_service_Fiber optic (Serviço de Internet Fibra Óptica): Surpreendentemente, clientes com fibra óptica também mostram uma tendência maior a evadir, sugerindo possíveis problemas de qualidade de serviço ou expectativas não atendidas.

monthly_charges (Cobranças Mensais): Mensalidades mais altas tendem a aumentar a probabilidade de churn.

Serviços Adicionais (online_security, tech_support, online_backup): A ausência ou não adesão a esses serviços está correlacionada com maior churn, indicando que clientes com mais serviços tendem a ser mais fiéis.

## 💡 Recomendações Estratégicas para Telecom X
Com base nos insights obtidos pelos modelos preditivos, sugiro as seguintes ações para a Telecom X:

Foco em Clientes Recém-Chegados: Implementar programas de boas-vindas aprimorados e acompanhamento proativo nos primeiros meses de contrato (tenure), oferecendo suporte e incentivando a adesão a serviços adicionais.

Incentivo a Contratos de Longo Prazo: Criar ofertas e benefícios atraentes para migração de clientes de planos mensais para contratos anuais ou bianuais, destacando a estabilidade e o custo-benefício.

Otimização do Método de Pagamento: Investigar as causas da insatisfação associada ao "Cheque Eletrônico". Pode ser necessário melhorar a experiência do usuário com este método ou promover ativamente alternativas mais convenientes e seguras.

Melhoria na Qualidade da Fibra Óptica: Realizar uma análise aprofundada da experiência dos clientes de fibra óptica. Pesquisas de satisfação e monitoramento da qualidade do serviço podem revelar pontos de dor e oportunidades de melhoria.

Promoção de Serviços Agregados: Destacar o valor e a segurança dos serviços adicionais (segurança online, suporte técnico, backup) para aumentar a adesão e, consequentemente, a fidelidade do cliente.

Revisão da Estrutura de Preços: Avaliar a competitividade dos planos com mensalidades elevadas, considerando a oferta de pacotes mais flexíveis ou descontos para clientes de alto gasto, garantindo que o valor percebido justifique o custo.

## 🛠️ Tecnologias Utilizadas
Python

Pandas

NumPy

Seaborn

Matplotlib

Scikit-learn

Imbalanced-learn (imblearn)


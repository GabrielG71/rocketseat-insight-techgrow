# Previsão de Churn --- SaaS

Este projeto documenta a construção de um **pipeline completo de análise
e modelagem preditiva** para identificar clientes com maior
probabilidade de cancelamento (**churn**) em um produto SaaS.

O objetivo é demonstrar domínio em:

- Análise exploratória de dados (EDA)
- Preparação e transformação de dados
- Encoding de variáveis categóricas
- Padronização de variáveis numéricas
- Separação de dados em treino e teste
- Treinamento e comparação de modelos de Machine Learning
- Avaliação com métricas de classificação
- Interpretação dos resultados para suporte à tomada de decisão

---

## Contexto

Cada linha do dataset representa um cliente de um produto SaaS e seu
comportamento de uso.

O objetivo é prever quais clientes têm maior probabilidade de cancelar o
serviço para permitir ações preventivas de retenção.

## Dataset

O dataset utilizado (`base_churns.csv`) contém as
seguintes variáveis:

### Variáveis

- **tempo_contrato_meses**: tempo de contrato do cliente
- **plano**: tipo de plano contratado
- **regiao**: região do cliente
- **logins_mes**: número médio de logins por mês
- **tickets_suporte**: quantidade de tickets de suporte abertos
- **valor_mensal**: valor mensal pago pelo cliente
- **inadimplencia**: indicador de inadimplência (0 ou 1)
- **qtd_funcionarios**: tamanho da empresa cliente
- **uso_media_diaria_horas**: tempo médio de uso diário da plataforma
- **churn**: variável alvo indicando cancelamento do serviço

---

## Etapas do Projeto

### 1) Importação e exploração dos dados

Foram realizadas inspeções iniciais para entender a estrutura do
dataset:

- `head()` para visualizar registros
- `info()` para verificar tipos de variáveis
- `describe()` para estatísticas descritivas
- verificação de valores nulos

Também foram criadas visualizações para analisar distribuições e
diferenças entre clientes que cancelaram e os que permaneceram.

---

### 2) Preparação e tratamento dos dados

As seguintes transformações foram aplicadas:

- Remoção da coluna identificadora `id_cliente`
- Encoding de variáveis categóricas (`plano`, `regiao`) com **One-Hot
  Encoding**
- Padronização das variáveis numéricas utilizando **StandardScaler**
- Análise de correlação para identificar possíveis variáveis
  redundantes

```python
df = pd.get_dummies(df, columns=["plano","regiao"], drop_first=True)
```

---

### 3) Separação dos dados

Os dados foram divididos em:

- **70% para treino**
- **30% para teste**

A variável **churn** foi definida como target.

```python
X = df.drop(columns=["churn"])
y = df["churn"]
```

---

### 4) Treinamento dos modelos

Foram treinados três modelos de classificação:

- **Regressão Logística** (modelo baseline)
- **Random Forest**
- **XGBoost**

O objetivo foi comparar desempenho e capacidade de generalização.

---

### 5) Avaliação dos modelos

Os modelos foram avaliados utilizando métricas padrão de classificação:

- accuracy
- precision
- recall
- f1-score
- roc_auc_score

Também foram geradas:

- **matriz de confusão**
- **curva ROC**

para análise visual do desempenho.

---

## Principais Resultados

- Os modelos conseguiram identificar padrões de comportamento
  associados ao churn.
- Variáveis relacionadas a **uso da plataforma**, **tempo de
  contrato** e **inadimplência** mostraram forte relação com
  cancelamentos.
- Modelos baseados em árvores (Random Forest e XGBoost) apresentaram
  desempenho superior ao modelo linear baseline.

Essas informações permitem que o time de produto identifique clientes de
risco e implemente estratégias de retenção.

---

## Como executar

### 1) Criar ambiente virtual

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 2) Instalar dependências

```bash
pip install pandas matplotlib seaborn scikit-learn xgboost jupyter
```

### 3) Executar o notebook

```bash
jupyter notebook insights_final.ipynb
```

---

## Tecnologias

- Python
- Pandas
- Seaborn / Matplotlib
- Scikit-learn
- XGBoost
- Jupyter Notebook

---

## Autor

Projeto desenvolvido por Gabriel Gonçalves como parte de estudos em
análise e modelagem de dados.

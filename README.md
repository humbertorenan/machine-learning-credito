# 🏦 Projeto de Machine Learning: Previsão de Aprovação de Crédito e Risco

## Visão Geral

Este projeto é uma análise de dados e um modelo de Machine Learning focado em **prever o risco de inadimplência (mau pagador)** para a concessão de crédito. O objetivo principal é classificar os solicitantes como bom ou mau pagador, usando dados demográficos e de histórico de aplicação de cartão de crédito.

O trabalho segue um fluxo completo de ML: Análise Exploratória (EDA), Pré-processamento, Engenharia de Recursos (Feature Engineering), Treinamento de Modelo (Regressão Logística) e Avaliação de Performance.

## 💾 Fonte dos Dados

Os dados utilizados foram extraídos do Kaggle, provenientes de duas fontes:
1.  **`application_record.csv`**: Informações demográficas e de aplicação de crédito dos clientes.
2.  **`credit_record.csv`**: Histórico mensal de pagamento dos clientes (utilizado para criar a variável-alvo).

## 🚀 Etapas do Projeto

O projeto foi executado seguindo os seguintes passos principais:

### 1. Preparação e Criação da Variável-Alvo (`TARGET`)
* **Merge dos DataFrames:** As tabelas de aplicação e histórico de crédito foram unidas pelo `ID` do cliente.
* **Definição do Risco:** A variável-alvo (`TARGET`) foi criada a partir do histórico de pagamento:
    * **`TARGET = 1` (Mau Pagador):** Clientes que apresentaram qualquer status de atraso grave (2, 3, 4 ou 5 meses) no histórico.
    * **`TARGET = 0` (Bom Pagador):** Clientes que mantiveram status de pagamento em dia (0 ou 1) ou sem dívida (C/X).

### 2. Pré-processamento e Limpeza de Dados
* **Tratamento de Nulos:** Valores ausentes em `OCCUPATION_TYPE` foram preenchidos com 'Others'. Valores de contagem (`AMT_REQ_CREDIT_BUREAU_...`) foram preenchidos com zero.
* **Codificação Categórica:**
    * Variáveis binárias (Y/N) foram mapeadas para `1/0`.
    * Variáveis nominais (Ex: `NAME_INCOME_TYPE`, `EDUCATION`) foram transformadas usando *One-Hot Encoding* (`pd.get_dummies`).

### 3. Engenharia de Recursos (Feature Engineering)
As colunas de tempo (dias) foram transformadas em variáveis mais interpretáveis:
* `AGE_YEARS`: Idade do cliente em anos.
* `YEARS_EMPLOYED`: Tempo de emprego em anos.
* `INCOME_PER_FAMILY_MEMBER`: Razão da Renda Total pelo Número de Membros da Família.

### 4. Modelagem e Avaliação
* **Separação:** Os dados foram divididos em conjuntos de treino e teste (70/30) com `stratify=y` para manter a proporção da classe-alvo.
* **Escalonamento:** As *features* foram padronizadas usando `StandardScaler`.
* **Modelo:** Uma **Regressão Logística** foi treinada nos dados escalonados.

### Curva ROC (Receiver Operating Characteristic)
A Curva ROC demonstra o *trade-off* entre a Taxa de Verdadeiro Positivo (sensibilidade) e a Taxa de Falso Positivo.

## 🛠️ Tecnologias Utilizadas

* **Linguagem:** Python
* **Bibliotecas:** `pandas`, `kagglehub`, `os`
* **Machine Learning:** `scikit-learn` (`LogisticRegression`, `StandardScaler`, `train_test_split`, `metrics`)
* **Visualização:** `matplotlib.pyplot`

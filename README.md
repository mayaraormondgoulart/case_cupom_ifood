
# 📦 iFood Case — Análise de Campanha com Cupons

Este projeto realiza uma **análise completa de uma campanha de cupons no iFood**, combinando **teste A/B**, **estatística aplicada**, **análise financeira (ROI e LTV)** e **segmentação de usuários** para avaliar o impacto da ação em métricas comportamentais e de negócio.

A análise foi desenvolvida utilizando **PySpark**, bibliotecas estatísticas em Python e técnicas de Machine Learning para suportar decisões orientadas a dados.

---

## 🧩 Contexto do Problema

No iFood, diferentes áreas utilizam testes A/B para validar hipóteses de crescimento e avaliar o impacto de novas iniciativas.  
Neste case, foi fornecida uma base de pedidos contendo uma **marcação de usuários em grupo controle e grupo target**, onde o grupo target recebeu um **cupom promocional**.

Os objetivos principais foram:

1. Avaliar se a campanha teve **impacto significativo**;
2. Analisar a **viabilidade financeira** da iniciativa;
3. Criar **segmentações de clientes** relevantes para o teste;
4. Propor **melhorias e próximos passos**.

---

## 📋 Premissas

- O **iFood financiou 100% do valor do cupom**;
- O valor do cupom **não está refletido diretamente no valor do pedido** — a coluna `discount` encontra-se zerada na base original;
- O objetivo da campanha **não é lucro imediato**, mas sim **aumentar retenção e LTV** no médio e longo prazo;
- A **margem de contribuição** adotada na análise é de **25%**.

---

## 🛠️ Etapas do Projeto

### 1️⃣ Preparação e Limpeza dos Dados
- Validação de schema e tipos de dados;
- Correção de formatações conforme documentação;
- Garantia de consistência no número de registros;
- Tratamento de valores nulos;
- Criação de chaves auxiliares;
- Preparação da base analítica por cliente (`customer_id`).

---

### 2️⃣ Análise Exploratória (EDA)
Foram analisadas distribuições, estatísticas descritivas e outliers das principais variáveis numéricas, como:
- Valor total do pedido;
- Frequência de compra;
- Ticket médio;
- Recência;
- Valor total gasto.

#### Tratamento de Outliers
Foram testados dois métodos:
- Corte por percentil (P99);
- Método do Intervalo Interquartil (IQR).

O **IQR** foi escolhido por ser mais robusto para distribuições assimétricas e preservar melhor o comportamento central dos dados.

---

### 3️⃣ Construção da Base Analítica Final
Foi criada uma base agregada por **customer_id**, contendo, por exemplo:
- Quantidade de pedidos;
- Frequência mensal;
- Ticket médio;
- Valor total gasto;
- Recência (mediana do tempo entre pedidos).

Essa base foi utilizada tanto no teste A/B quanto na segmentação.

---

## 🧪 Teste A/B — Métricas Avaliadas

As métricas foram comparadas entre **grupo controle** e **grupo target**, com testes estatísticos adequados:

- **Retenção** → teste de proporções (z-test);
- **Frequência de pedidos** → teste Mann-Whitney / t-test;
- **Ticket médio** → t-test;
- **Recência (tempo entre pedidos)** → Mann-Whitney;
- **Valor total gasto por cliente** → t-test.

### 📈 Principais Resultados

- **Retenção**: aumento estatisticamente significativo no grupo target;
- **Frequência**: aumento significativo no número de pedidos;
- **Ticket médio**: sem diferença estatisticamente significativa;
- **Recência**: redução do tempo entre pedidos no grupo target;
- **Valor total gasto**: uplift significativo no grupo target.

👉 A campanha alterou o **comportamento de compra**, e não o preço médio.

---

## 💰 Análise de Viabilidade Financeira

### Premissas Financeiras
- Custo do cupom: **R$ 10,00 por usuário**;
- Margem de contribuição: **25%**;
- Análise separada em **curto prazo (período do teste)** e **longo prazo (LTV)**.
---

## 🧠 Segmentação de Usuários

Foi aplicada segmentação via **KMeans**, utilizando variáveis comportamentais e financeiras:
- Quantidade de pedidos;
- Frequência;
- Ticket médio;
- Recência;
- Valor total gasto;
- Tempo de vida;
- Diversidade de restaurantes.

### Definição do número de clusters
- Método do cotovelo (Elbow Method);
- Índice de Calinski-Harabasz.

📌 O valor **k = 3** foi escolhido por apresentar o melhor equilíbrio entre separação estatística e interpretabilidade de negócio.

---

## ⚙️ Requisitos

Para executar o notebook, é necessário:

- Python ≥ 3.8  
- Apache Spark (via `pyspark`)  

### Bibliotecas Python
```bash
pip install pyspark pandas matplotlib seaborn scikit-learn statsmodels scipy


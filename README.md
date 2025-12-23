# 📊 Case iFood — Teste A/B, Análise Financeira e Segmentação de Usuários

Este projeto tem como objetivo analisar o impacto de uma **campanha de cupons** utilizando um **teste A/B**, avaliando efeitos em métricas comportamentais, financeiras e de retenção de usuários.  
Além disso, são propostas **segmentações de clientes** e **recomendações estratégicas** com base nos resultados obtidos.

---

## 🧩 Contexto do Problema

No iFood, testes A/B são amplamente utilizados para validar hipóteses de crescimento e avaliar o impacto de novas iniciativas em métricas-chave do negócio.  

Neste case, foi disponibilizada uma base de pedidos contendo uma **marcação de usuários em grupo controle e grupo target**, onde o grupo target recebeu um **cupom promocional**.

Os principais objetivos da análise são:

1. Avaliar se a campanha teve **impacto estatisticamente significativo**;
2. Analisar a **viabilidade financeira** da iniciativa;
3. Criar **segmentações de usuários** para aprofundar a análise;
4. Propor **próximos passos e melhorias** para novos testes A/B.

---

## 🛠️ Etapas do Projeto

### 1️⃣ Preparação e Limpeza dos Dados
- Validação de schema e tipos de dados;
- Correção de formatações conforme documentação;
- Garantia de consistência no número de registros;
- Tratamento de valores nulos;
- Criação de chaves e métricas auxiliares.

---

### 2️⃣ Análise Exploratória (EDA)
Foram analisadas distribuições, estatísticas descritivas e outliers das principais variáveis numéricas, como:
- Valor total do pedido;
- Frequência de compra;
- Ticket médio;
- Recência.

#### Tratamento de Outliers
Foram testados dois métodos:
- Corte por percentil (P99);
- Método do Intervalo Interquartil (IQR).

O **IQR** foi escolhido por ser mais robusto para distribuições assimétricas e preservar melhor o comportamento central dos dados.

---

### 3️⃣ Construção da Base Analítica Final
Foi criada uma base agregada por **customer_id**, contendo métricas como:
- Quantidade de pedidos;
- Frequência mensal;
- Ticket médio;
- Valor total gasto;
- Recência (mediana do tempo entre pedidos);
- Tempo de vida do cliente;
- Número de restaurantes distintos;
- Marcação de grupo (control × target).

Essa base serviu como insumo para o teste A/B e para a segmentação.

---

## 🧪 Teste A/B — Métricas Avaliadas

As métricas foram comparadas entre **grupo controle** e **grupo target**, com testes estatísticos apropriados:

- **Retenção** → teste de proporções (z-test)
- **Frequência de pedidos** → teste Mann-Whitney / t-test
- **Ticket médio** → t-test
- **Recência** (tempo entre pedidos) → Mann-Whitney
- **Valor total gasto por cliente** → t-test

### 📈 Principais Resultados

- **Retenção**: aumento estatisticamente significativo no grupo target;
- **Frequência**: aumento significativo de pedidos por usuário;
- **Ticket médio**: sem diferença estatisticamente significativa;
- **Recência**: usuários target compram com menor intervalo entre pedidos;
- **Valor total gasto**: uplift significativo no grupo target.

👉 A campanha impactou o **comportamento de compra**, não o preço médio.

---

## 💰 Análise de Viabilidade Financeira

### Premissas adotadas:
- Custo do cupom: **R$ 10,00 por usuário**, financiado integralmente pelo iFood;
- Margem de contribuição: **25%**;
- Objetivo da campanha: **retenção e aumento de LTV**, não lucro imediato.

### Resultados:
- O **resultado de curto prazo** pode ser negativo devido ao custo do incentivo;
- O **LTV incremental por usuário é positivo**, sustentado por maior retenção e frequência;
- O ROI total se torna positivo quando considerado o **impacto de longo prazo**.

👉 A campanha é **financeiramente viável sob a ótica de LTV**.

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
- Método do cotovelo (Elbow);
- Índice de Calinski-Harabasz.

📌 O valor **k = 3** foi escolhido por apresentar o melhor equilíbrio entre separação estatística e interpretabilidade de negócio.

Os clusters representam perfis distintos de usuários (baixo, médio e alto engajamento).

---

## 🚀 Próximos Passos Recomendados

- Avaliar o impacto do cupom **por segmento de usuário**;
- Criar campanhas diferenciadas para cada cluster;
- Testar cupons com **valores variáveis** conforme perfil;
- Avaliar efeitos de longo prazo com janelas maiores;
- Integrar métricas de churn e reincidência em novos testes.

---

## 📌 Conclusão

A campanha de cupons:
- **Aumentou retenção, frequência e LTV**;
- Não elevou artificialmente o ticket médio;
- Mostra-se uma **alavanca sustentável de crescimento**, quando bem segmentada.

O uso combinado de **teste A/B, análise estatística e segmentação** permitiu uma visão completa do impacto da iniciativa, apoiando decisões orientadas a dados.

---

📍 *Este projeto foi desenvolvido como parte de um desafio analítico, com foco em tomada de decisão baseada em dados, estatística aplicada e visão de negócio.*

# 📊 Dashboard Comercial — Power BI

## 📌 Sobre o Projeto

Projeto de análise comercial desenvolvido no Power BI com foco em:

- Monitoramento de vendas
- Controle logístico
- Performance de fornecedores
- Análise operacional
- Indicadores estratégicos comerciais

O dashboard foi estruturado utilizando modelagem dimensional (Star Schema), permitindo análises eficientes e escaláveis.

---

# 🎯 Objetivo

Transformar dados brutos oriundos de planilhas Excel em informações estratégicas para suporte à tomada de decisão comercial e logística.

---

# 🛠️ Ferramentas Utilizadas

- Power BI
- Power Query
- DAX
- Excel
- Modelagem Dimensional

---
---

# 🔄 Tratamento de Dados — Power Query

Durante o processo ETL foram realizadas as seguintes etapas:

- Remoção de arquivos em branco
- Limpeza de registros inválidos
- Padronização das tabelas
- Ajuste de tipos de dados
- Estruturação entre fato e dimensões

---

# 🧠 Modelagem de Dados

O projeto foi desenvolvido utilizando o conceito de:

## ⭐ Star Schema (Modelo Estrela)

### Relacionamentos

| Origem | Destino | Cardinalidade |
|---|---|---|
| dProdutos | fVendas | 1:N |
| dColaborador | fVendas | 1:N |
| dFornecedor | fVendas | 1:N |

---
# 🧮 Colunas Calculadas — DAX

## 🔹 Custo da Compra

Relaciona o custo do produto com a quantidade comprada.

```DAX
Custo da Compra =
RELATED(dProdutos[Custo Total]) * fVendas[Quantidade]
```

---

## 🔹 Status da Entrega

Responsável por identificar se a entrega ocorreu dentro do prazo previsto.

```DAX
Status =
IF(
    [Entrega Realizada] > [Previsão de Entrega];
    "Atrasada";
    "No Prazo"
)
```

---

# 📈 Medidas Criadas — DAX

## 🔹 Total de Gastos

```DAX
Total de gastos =
SUM(fVendas[Custo da Compra])
```

---

## 🔹 Ticket Médio

```DAX
Ticket medio =
AVERAGE(fVendas[Custo da Compra])
```

---

## 🔹 Compras Realizadas

```DAX
Compras Realizadas =
COUNTROWS(fVendas)
```

---

## 🔹 Percentual de Compras no Prazo

```DAX
% Compras no Prazo =
CALCULATE(
    [Compras Realizadas];
    fVendas[Status] = "No Prazo"
)
/ [Compras Realizadas]
```

> Formatação aplicada: Percentual (%)

---

## 🔹 Percentual de Compras Atrasadas

```DAX
% Compras Atrasadas =
CALCULATE(
    [Compras Realizadas];
    fVendas[Status] = "Atrasada"
)
/ [Compras Realizadas]
```

> Formatação aplicada: Percentual (%)

---
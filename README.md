# 📊 Dashboard Comercial — Power BI

## 📌 Sobre o Projeto

Projeto de Business Intelligence desenvolvido no Power BI com foco em análise comercial, logística e operacional, utilizando dados importados de planilhas Excel.

O dashboard foi estruturado utilizando modelagem dimensional no formato Star Schema (Modelo Estrela), permitindo análises eficientes, organizadas e escaláveis.

O objetivo principal é transformar dados operacionais em informações estratégicas para apoio à tomada de decisão.

---

# 🎯 Objetivos do Projeto

- Monitorar compras realizadas
- Acompanhar custos operacionais
- Avaliar desempenho logístico
- Identificar atrasos de entrega
- Analisar fornecedores
- Criar indicadores estratégicos comerciais
- Desenvolver visualizações interativas e executivas

---

# 🛠️ Ferramentas Utilizadas

- Power BI
- Power Query
- DAX
- Excel
- Modelagem Dimensional

---

# 📂 Estrutura das Tabelas

## 🔹 Tabela Fato

### `fVendas`

Tabela central responsável pelos registros comerciais.

| Campo |
|---|
| Pedido |
| Data Compra |
| Data Expedição |
| Previsão de Entrega |
| Entrega Realizada |
| Colaborador |
| Produto |
| Quantidade |
| Fornecedor |

---

## 🔹 Tabelas Dimensão

### `dProdutos`

| Campo |
|---|
| Código |
| Produto |
| Custo |
| Custo Transporte |

---

### `dColaborador`

| Campo |
|---|
| Codigo Comprador |
| Nome Comprador |

---

### `dFornecedor`

| Campo |
|---|
| Código |
| Fornecedor |

---

# 🔄 Processo ETL — Power Query

Durante o processo de transformação dos dados foram realizadas as seguintes etapas:

- Importação das planilhas Excel
- Remoção de arquivos em branco
- Limpeza de registros inválidos
- Ajuste de tipos de dados
- Padronização das tabelas
- Organização entre fato e dimensões

---

# 🧠 Modelagem de Dados

O modelo foi desenvolvido utilizando o conceito de:

# ⭐ Star Schema (Modelo Estrela)

## Relacionamentos

| Origem | Destino | Cardinalidade |
|---|---|---|
| dProdutos | fVendas | 1:N |
| dColaborador | fVendas | 1:N |
| dFornecedor | fVendas | 1:N |

A modelagem dimensional foi utilizada para:
- Melhorar performance
- Facilitar análises
- Otimizar medidas DAX
- Garantir escalabilidade do dashboard

---

# 🧮 Colunas Calculadas — DAX

## 🔹 Custo da Compra

Responsável por calcular o custo total de cada compra com base na quantidade adquirida.

```DAX
Custo da Compra =
RELATED(dProdutos[Custo Total]) * fVendas[Quantidade]
```

---

## 🔹 Status da Entrega

Responsável por identificar se a entrega ocorreu dentro ou fora do prazo previsto.

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

# 📊 Visualizações Desenvolvidas

O dashboard foi construído com foco em análise visual, interatividade e experiência do usuário.

## 📌 Elementos Visuais Criados

### 🔹 Cartões KPI
Foram desenvolvidos 3 cartões para exibição dos principais indicadores:

- Total de Gastos
- Ticket Médio
- Compras Realizadas

---

### 🔹 Gráfico de Matriz

Utilizado para análise detalhada das informações comerciais e operacionais.

Permite:
- Comparações entre fornecedores
- Visualização por produto
- Análise de volumes
- Organização hierárquica das informações

---

### 🔹 Gráfico de Área

Utilizado para acompanhamento temporal dos dados e identificação de tendências.

Possibilita:
- Visualização da evolução das compras
- Comparação entre períodos
- Identificação de crescimento ou queda operacional

---

### 🔹 Gráfico de Colunas Clusterizado

Desenvolvido para comparação entre categorias e análise comparativa de desempenho.

Aplicações:
- Comparação entre fornecedores
- Comparação entre produtos
- Volume de compras por categoria

---

### 🔹 Gráfico de Barras Clusterizado

Utilizado para análises comparativas horizontais e ranking de informações.

Aplicações:
- Ranking de fornecedores
- Produtos com maior volume
- Comparações operacionais

---

### 🔹 Segmentação de Dados (Slicers)

Foram implementadas segmentações para facilitar a navegação e análise dinâmica do dashboard.

Exemplos:
- Produto
- Fornecedor
- Status da entrega
- Período

---

# 🎨 Formatação Visual do Dashboard

Foi realizada personalização visual completa dos elementos do dashboard visando melhor experiência do usuário e apresentação executiva.

## Ajustes realizados

- Padronização visual dos gráficos
- Ajuste de cores
- Configuração de fontes
- Alinhamentos dos elementos
- Organização visual das páginas
- Melhoria da legibilidade
- Padronização dos títulos
- Configuração de rótulos e legendas

O objetivo foi criar um dashboard:
- limpo
- intuitivo
- profissional
- visualmente organizado

---

# 📈 Indicadores do Projeto

## 💰 Financeiro
- Total de Gastos
- Ticket Médio
- Custos Operacionais

## 🚚 Logístico
- Compras no Prazo
- Compras Atrasadas
- Performance de Entrega

## 📦 Comercial
- Quantidade de Compras
- Volume por Produto
- Volume por Fornecedor

---

# 🔍 Possíveis Insights Gerados

O dashboard possibilita identificar:

- Fornecedores com maior índice de atraso
- Produtos com maior custo operacional
- Tendência de compras ao longo do tempo
- Volume operacional por fornecedor
- Eficiência logística
- Relação entre quantidade e custo
- Desempenho operacional das compras

---

# 🚀 Como Executar o Projeto

## 1️⃣ Clonar o repositório

```bash
git clone https://github.com/nerydyego/Power_Bi_Comercial
```

---

## 2️⃣ Abrir o arquivo Power BI

Abrir o arquivo `.pbix` no Power BI Desktop.

---

## 3️⃣ Atualizar os dados

Caso necessário:
- Atualizar conexões
- Verificar caminhos das planilhas
- Aplicar atualização dos dados

---

# 📌 Status do Projeto

✅ Estrutura de dados concluída  
✅ Modelagem dimensional concluída  
✅ Criação das medidas DAX concluída  
✅ Construção inicial do dashboard concluída  
🚧 Projeto em evolução

---

# 👨‍💻 Autor

Dyego Nery

## 🔗 Contatos

- LinkedIn: www.linkedin.com/in/dyego-nery
- GitHub: [Adicionar](https://github.com/nerydyego)

---
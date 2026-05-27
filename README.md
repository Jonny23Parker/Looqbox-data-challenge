# 🚀 Looqbox Data Challenge – Solução Completa

[![MySQL](https://img.shields.io/badge/MySQL-8.0-blue?logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Python](https://img.shields.io/badge/Python-3.9%2B-green?logo=python&logoColor=white)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Pandas-2.0-blue?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-3.7-orange)](https://matplotlib.org/)
[![Seaborn](https://img.shields.io/badge/Seaborn-0.12-teal)](https://seaborn.pydata.org/)
[![Google Colab](https://img.shields.io/badge/Google_Colab-F9AB00?logo=googlecolab&logoColor=white)](https://colab.research.google.com/)

**Autor:** Jonatas de Siqueira  
**Data:** 27 de Maio de 2026  
**Desafio:** Data Analytics & Engineering Challenge – Looqbox

---

## 📋 Sobre o Projeto

Este repositório contém minha solução completa para o **Desafio Técnico da Looqbox** – uma empresa de tecnologia pioneira em **Search Driven Analytics** e democratização do acesso a dados.

O desafio consistiu em:

- ✅ Acessar e explorar um banco de dados MySQL com informações de vendas, produtos e lojas
- ✅ Responder 3 perguntas de negócio utilizando SQL
- ✅ Criar uma função dinâmica em Python para consultas parametrizadas
- ✅ Processar queries prontas e gerar visualização estratégica
- ✅ Analisar uma base de dados IMDB e criar visualizações com justificativa

**Link para o arquivo do colab disponivel em:* 

(https://colab.research.google.com/drive/1GmlGYDMPIAC2nUNopRkdCbTqv-oan4sI)

*Necessita de credencias de acesso para executar os códigos*

---

## 🎯 Habilidades Demonstradas

| Área | Tecnologias / Conceitos |
|------|------------------------|
| **SQL** | Queries complexas, CTEs, Joins, Agregações, Otimização |
| **Python** | Pandas, MySQL Connector, Funções dinâmicas, Tratamento de erros |
| **Visualização** | Matplotlib, Seaborn, Storytelling com dados |
| **Engenharia de Dados** | Conexão a bancos, ETL, Automação de consultas |
| **Boas Práticas** | Versionamento (Git), Documentação, Código modular |

---

## 🗂️ Estrutura do Projeto

```plaintext
looqbox-challenge/
│
├── README.md                          # Documentação completa
│
├── sql/
│   ├── 01_top_10_products.sql         # 10 produtos mais caros
│   ├── 02_sections_by_dept.sql        # Seções de BEBIDAS e PADARIA
│   └── 03_sales_by_business.sql       # Vendas por Business Area (Q1 2019)
│
├── notebooks/
│   └── looqbox_challenge_colab.ipynb  # Google Colab (versão interativa)
│
├── images/
│   ├── q4_2019_sales_by_business.png  # Vendas Q4 2019
│   ├── imdb_rating_distribution.png   # Distribuição das notas IMDB
│   ├── imdb_top_genres.png            # Top 10 gêneros
│   └── imdb_ratings_by_year.png       # Tendência de notas por ano
│
└── reports/
    └── looqbox_challenge_report.pdf   # Relatório final (PDF)
```


---

## 📊 Perguntas de Negócio (SQL)


### 1️⃣ Quais os 10 produtos mais caros da empresa?

```
SELECT 
    PRODUCT_COD,
    PRODUCT_NAME,
    PRODUCT_VAL,
    DEP_NAME,
    SECTION_NAME
FROM data_product
ORDER BY PRODUCT_VAL DESC
LIMIT 10;
```

---


### 2️⃣ Quais seções os departamentos 'BEBIDAS' e 'PADARIA' possuem?
```
SELECT 
    DEP_NAME,
    SECTION_NAME,
    SECTION_COD
FROM data_product
WHERE DEP_NAME IN ('BEBIDAS', 'PADARIA')
GROUP BY DEP_NAME, SECTION_NAME, SECTION_COD
ORDER BY DEP_NAME, SECTION_NAME;
```

---


### 3️⃣ Total de vendas por Business Area no 1º trimestre de 2019

```
SELECT 
    ds.BUSINESS_NAME,
    SUM(dss.SALES_VALUE) AS TOTAL_SALES
FROM data_store_sales dss
INNER JOIN data_store_cad ds ON dss.STORE_CODE = ds.STORE_CODE
WHERE dss.DATE BETWEEN '2019-01-01' AND '2019-03-31'
GROUP BY ds.BUSINESS_NAME
ORDER BY TOTAL_SALES DESC;
```

Resultado: O setor Farma lidera com R$ 81,7 milhões, seguido por Varejo (R$ 81,0 milhões) e Atacado (R$ 80,4 milhões).

---


🐍 Função Dinâmica: retrieve_data()
Função flexível e reutilizável para consultar a tabela data_product_sales com 3 parâmetros opcionais.


---


Assinatura

```
def retrieve_data(product_code=None, store_code=None, date=None):
    """
    Retorna DataFrame com filtros dinâmicos.
    
    Parâmetros:
    - product_code: int ou list (código do produto)
    - store_code: int ou list (código da loja)
    - date: list ['YYYY-MM-DD', 'YYYY-MM-DD'] (intervalo)
    """
```

---


Diferenciais Implementados
✅ Suporte a valores únicos ou listas

✅ Prevenção contra SQL Injection (parametrização)

✅ Tratamento de erros e conexões

✅ Retorno em DataFrame padronizado


---


📈 Visualizações Geradas

1. Vendas por Business Area – Q4 2019
![Vendas2019](https://github.com/Jonny23Parker/Looqbox-data-challenge/blob/master/images/q4_2019_sales_by_business.png)

Justificativa: Gráfico de barras horizontal para fácil comparação entre áreas de negócio. Valores anotados para clareza executiva.

---


2. Distribuição das Avaliações – IMDB
![distribuicao](https://github.com/Jonny23Parker/Looqbox-data-challenge/blob/master/images/imdb_rating_distribution.png)

Justificativa: Histograma com KDE para identificar padrão de notas. Linhas da média (6,77) e mediana (7,00) destacadas para referência estatística.

---


3. Top 10 Gêneros – IMDB
![top10](https://github.com/Jonny23Parker/Looqbox-data-challenge/blob/master/images/imdb_top_genres.png)

Justificativa: Barras horizontais para facilitar leitura dos rótulos de gênero. Útil para times de conteúdo.

---


4. Avaliações por Ano – IMDB
![Avaliacao](https://github.com/Jonny23Parker/Looqbox-data-challenge/blob/master/images/imdb_ratings_by_year.png)

Justificativa: Dispersão + linha de tendência para mostrar evolução temporal da qualidade dos filmes.

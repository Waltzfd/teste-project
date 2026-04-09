# 🚀 Sistema de Monitoramento de Reclamações + Impacto no Negócio

## 📌 Visão Geral
Este projeto foi desenvolvido para analisar reclamações (de clientes ou funcionários) e prever o impacto direto no desempenho do negócio, como vendas e produtividade. É um projeto ponta-a-ponta que conecta três pilares essenciais:

*   **Engenharia de Dados:** Coleta e estruturação.
*   **Análise de Dados:** Geração de insights e métricas.
*   **Machine Learning:** Modelagem preditiva.

---

## 🧠 Objetivo
Construir um pipeline automatizado capaz de:
1. Coletar dados de fontes externas.
2. Tratar, limpar e organizar informações em um banco relacional.
3. Analisar padrões e tendências de mercado/setor.
4. Gerar insights acionáveis via dashboards.
5. Realizar previsões inteligentes utilizando Machine Learning.

---

## 🧱 Arquitetura e Etapas

### 1. 📥 Coleta de Dados (Data Acquisition)
Fontes de dados sugeridas para o projeto:
*   **Web Scraping:** Reclame Aqui (usando `BeautifulSoup`).
*   **Datasets:** Kaggle ou repositórios públicos.
*   **Governamentais:** API do [dados.gov.br](https://dados.gov.br).

**Principais Atributos:** Data da reclamação, Empresa/Setor, Categoria do problema e Avaliação/Nota.

### 2. 🗄️ Armazenamento (Data Engineering)
Utilização do **PostgreSQL** para persistência, com foco em modelagem relacional e normalização.

```sql
-- Exemplo de estrutura de tabelas
CREATE TABLE empresas (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(255),
    setor VARCHAR(100)
);

CREATE TABLE reclamacoes (
    id SERIAL PRIMARY KEY,
    empresa_id INT REFERENCES empresas(id),
    texto_reclamacao TEXT,
    data_criacao TIMESTAMP,
    status VARCHAR(50)
);

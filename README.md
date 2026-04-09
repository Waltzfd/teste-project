# 🚀 ReclameX: Monitoramento e Impacto de Marcas (Reclame Aqui)

## 📌 Visão Geral
Este projeto é focado na extração e análise de dados do **Reclame Aqui**. O objetivo é monitorar a reputação de empresas, entender as principais dores dos clientes e prever como a insatisfação impacta o negócio (como churn de clientes ou queda em vendas).

Integração de três pilares:
1.  **Engenharia de Dados:** Extração e estruturação de dados não estruturados.
2.  **Análise de Dados:** Identificação de tendências e gargalos de atendimento.
3.  **Machine Learning:** Classificação de sentimentos e predição de notas.

---

## 🧠 Objetivo
Construir um pipeline end-to-end que:
- Realiza o scraping de reclamações de empresas específicas.
- Organiza os dados para evitar duplicidade em cargas incrementais.
- Identifica os problemas mais recorrentes por setor.
- Prevê se uma reclamação tem alto potencial de virar uma "crise de imagem".

---

## 🧱 Arquitetura e Etapas

### 1. 📥 Coleta de Dados (Web Scraping)
Foco exclusivo na plataforma **Reclame Aqui**.
*   **Ferramentas:** Python com `BeautifulSoup`, `Selenium` ou `Scrapy`.
*   **Dados capturados:** 
    *   Título e texto da reclamação.
    *   Status (Respondida, Não respondida, Resolvida).
    *   Nota do consumidor e índice de "Voltaria a fazer negócio".
    *   Timestamp (Data e hora).

### 2. 🗄️ Armazenamento (Engenharia de Dados)
Modelagem relacional robusta no **PostgreSQL** para suportar análises históricas.

```sql
-- Estrutura sugerida para o projeto
CREATE TABLE empresas (
    id SERIAL PRIMARY KEY,
    nome_slug VARCHAR(255) UNIQUE, -- ex: 'magazine-luiza'
    setor VARCHAR(100)
);

CREATE TABLE reclamacoes (
    id_externo VARCHAR(50) PRIMARY KEY, -- ID único do Reclame Aqui
    empresa_id INT REFERENCES empresas(id),
    titulo VARCHAR(255),
    descricao TEXT,
    status VARCHAR(50),
    data_postagem TIMESTAMP,
    nota_final INT
);

```

3. 🔄 Pipeline de Dados (ETL / ELT)
Processamento: Python + Pandas para limpeza de strings e remoção de caracteres especiais.
Modelagem dbt:
src_reclamacoes: Dados crus do scraping.
stg_reclamacoes: Padronização de datas e categorias.
fct_insatisfacao: Tabela fato para alimentar o dashboard.
4. 📊 Dashboard de Insights
Visualização clara da saúde da marca utilizando Metabase ou Streamlit.

Métricas chave:
Tempo médio de resposta.
Volume de reclamações vs. Evolução da nota.
Nuvem de palavras dos termos mais citados (ex: "atraso", "estorno", "defeito").
5. 🤖 Machine Learning (NLP)
Análise de Sentimento: Classificar automaticamente se a reclamação é leve, moderada ou crítica.
Predição: Modelos para prever a probabilidade do cliente "voltar a fazer negócio" com base no texto inicial.
Ferramentas: scikit-learn, NLTK ou Spacy.
⚙️ Automação
Orquestração: Agendamento para rodar o scraper diariamente e atualizar os dados no banco usando cron ou Airflow.
Alertas: Envio de notificações via Telegram/Slack quando uma empresa monitorada recebe um pico de reclamações em curto espaço de tempo

### 3. 🔄 Pipeline de Dados (ETL / ELT)
*   **Processamento:** Python + Pandas para limpeza de strings e remoção de caracteres especiais.
*   **Modelagem dbt:**
    *   `src_reclamacoes`: Dados crus do scraping.
    *   `stg_reclamacoes`: Padronização de datas e categorias.
    *   `fct_insatisfacao`: Tabela fato para alimentar o dashboard.

---

### 4. 📊 Dashboard de Insights
Visualização clara da saúde da marca utilizando **Metabase** ou **Streamlit**.

*   **Métricas chave:**
    *   Tempo médio de resposta.
    *   Volume de reclamações vs. Evolução da nota.
    *   Nuvem de palavras dos termos mais citados (ex: `"atraso"`, `"estorno"`, `"defeito"`).

---

### 5. 🤖 Machine Learning (NLP)
*   **Análise de Sentimento:** Classificar automaticamente se a reclamação é leve, moderada ou crítica.
*   **Predição:** Modelos para prever a probabilidade do cliente "voltar a fazer negócio" com base no texto inicial.
*   **Ferramentas:** `scikit-learn`, `NLTK` ou `Spacy`.

---

## ⚙️ Automação
*   **Orquestração:** Agendamento para rodar o scraper diariamente e atualizar os dados no banco usando `cron` ou `Airflow`.
*   **Alertas:** Envio de notificações via Telegram/Slack quando uma empresa monitorada recebe um pico de reclamações em curto espaço de tempo.

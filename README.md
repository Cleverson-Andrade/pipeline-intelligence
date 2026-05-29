# SPR Pipeline Intelligence 🌽

> Dashboard analítico interativo para gestão do pipeline de híbridos de milho, desenvolvido durante estágio na área de **Dados / SPR** de uma empresa global do agronegócio.

---

## O Problema

A equipe de gerenciava dados do pipeline de híbridos dispersos entre um banco de dados em nuvem e múltiplas planilhas externas. Não havia uma visão unificada de classificação agronômica, perfis de risco, métricas de produtividade e custo de produção, o que tornava as decisões de avanço ou descarte (ADV/DROP) nos estágios finais do pipeline lentas e fora de padrão.

---

## A Solução

Pipeline de dados end-to-end integrando três fontes distintas em uma única interface analítica, entregue como um dashboard Streamlit multi-aba com deploy via CI/CD.

---

## Arquitetura

```
[Banco de Dados em Nuvem (PostgreSQL)]  ──>  ETL: Long → Wide (pivot)  ──>  [DataFrame Unificado]
                                                                                      ↑
[API de Planilhas Externas]  ─── Fonte de Decisões   ─ LEFT JOIN
                             ─── Fonte de Genética   ─ LEFT JOIN
                             ─── Fonte de Materiais  ─ LEFT JOIN
                                                                                      ↓
                                              [Dashboard Streamlit ─ 9 Abas Analíticas]
```

---

## Stack Tecnológica

| Camada | Tecnologia |
|---|---|
| Frontend | Streamlit + Highcharts (via `components.html`) |
| Processamento de dados | Python · pandas · NumPy |
| Banco de dados | PostgreSQL via SQLAlchemy + psycopg2 |
| Integração externa | Smartsheet Python SDK |
| Visualização | Plotly · Highcharts (JS embarcado) |
| Deploy | GitLab CI/CD + Position Connect |
| Identidade visual | CSS customizado (Brand Guidelines) |

---

## Funcionalidades

### Pipeline de Dados
- Leitura em **formato long** (uma linha por atributo por híbrido) e pivot para **formato wide** com chave composta
- A chave do pivot inclui sazonalidade
- **3 LEFT JOINs** com fontes externas
- Limpeza de caracteres invisíveis (zero-width space) que causavam falhas silenciosas nos joins
- Cache por sessão: 1h para banco de dados, 15min para APIs externas

### Dashboard — 9 Abas Analíticas

| Aba | Descrição |
|---|---|
| Explorador de Dados | Visão completa com filtros dinâmicos, colunas fixas, sort e exportação Excel/CSV |
| Performance de Híbridos | Classificação e performance por estágio e safra, com drill-down interativo |
| Risco Agronômico | Distribuição de risco, comparativo de genitores, heatmap por trait |
| Risco de Doenças | Tolerância ao enfezamento por estágio do pipeline e evolução por ano |
| Análise de Genitores | Recomendação, performance e grupo heterótico de fêmea e macho |
| Métricas de Produtividade | Yield médio por estágio, comparativo de cenários (melhor/médio/pior) |
| Custo de Produção | COGP (R$/sc) por estágio, ano e cenários de custo |
| Planejamento de Sementes | Redirecionamento ao dashboard de Planejamento de Produção |
| Qualidade de Grão | Risco de grãos ardidos por estágio e ano de avanço |

### UI/UX
- **Drill-down interativo**: clique em qualquer barra do gráfico para expandir a lista de híbridos
- **Tela cheia** em todos os gráficos via Fullscreen API
- Tabelas HTML customizadas: colunas fixas (sticky), badges de decisão, sort por coluna, seleção de célula
- Estado dos filtros persistido por sessão; botão de reset sem rerun indesejado
- Paleta de cores padronizada injetada via CSS global

---

## Impacto

- Consolidou 3 fontes de dados distintas em uma única interface analítica
- Eliminou o cruzamento manual entre banco de dados e planilhas
- Reduziu o tempo de preparação de análises de horas para segundos
- Adotado pela equipe de SPR como ferramenta padrão de análise de pipeline

---

---

## Variáveis de Ambiente

Veja `.env.example` para a lista completa de variáveis necessárias.

---

> **Nota:** Este repositório contém apenas a documentação e estrutura do projeto.  
> O código-fonte, dados e credenciais são proprietários e não estão incluídos.

---

## Autor

**Cleverson Moura**  
Estagiário em Data Science — SPR
[linkedin.com/in/seu-perfil](https://www.linkedin.com/in/cleversonmandrade/)

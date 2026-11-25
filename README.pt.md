# Despesa das famílias em Portugal (2022–2023)

[English](README.md) · Português

Como se distribui a despesa das famílias portuguesas e como varia entre regiões e níveis de rendimento? O projeto analisa a despesa anual média por agregado com dados do [Inquérito às Despesas das Famílias 2022/2023 do INE](https://ine.pt/xurl/pub/439486878).

## Principais resultados

- Habitação (39,3%), alimentação (12,9%) e transportes (12,1%) somam 64,3% da despesa média nacional.
- A habitação representa 39,3% da despesa com a renda subjetiva estimada pelas famílias, 34,1% com a renda imputada pelo modelo do INE e 16,4% quando se subtrai a renda subjetiva à despesa de habitação e à despesa total.
- No quinto quintil, a alimentação pesa menos no orçamento do que no primeiro (9,8% face a 15,8%), embora a despesa anual média com alimentação seja superior (3 442 € face a 2 571 €).

## Como reproduzir a análise

A execução foi verificada com Python 3.13 e SQLite 3.50. A consulta SQL de habitação requer SQLite 3.30 ou posterior, através do módulo `sqlite3` do Python.

A partir da raiz do repositório, em macOS ou Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install jupyterlab numpy pandas matplotlib openpyxl
cd notebooks
jupyter lab
```

Executa todas as células de cada notebook pela ordem abaixo, com a pasta `notebooks/` como diretório de trabalho do kernel.

1. [Limpeza e preparação](notebooks/01_limpeza_idef.ipynb) lê o Excel original e gera os dois CSV em [`data/processed/`](data/processed/).
2. [Análise exploratória](notebooks/02_analise_exploratoria.ipynb) lê os CSV e compara a estrutura da despesa por região e quintil, incluindo três cenários para a habitação.
3. [Análise SQL](notebooks/03_analise_sql.ipynb) carrega os mesmos CSV numa base SQLite em memória e responde a quatro perguntas sobre a despesa.

Os CSV já estão incluídos no repositório. Para explorar os resultados com esses ficheiros, podes começar pelo segundo ou pelo terceiro notebook.

## Dados e interpretação

- [Ficheiro Excel do INE](data/IDF20222023_a.xlsx). Os quadros Q.2.1.a e Q.2.1.b contêm a despesa em euros e em percentagem por região. Os quadros Q.2.11.a e Q.2.11.b apresentam as mesmas medidas por quintil.
- Os montantes de habitação e despesa total no cenário com renda imputada vêm do quadro «Em destaque: a avaliação da autolocação», na p. 36 da publicação. O cenário sem renda subjetiva conserva as restantes despesas não monetárias.
- Os quintis baseiam-se no rendimento equivalente de 2021 e as regiões seguem a delimitação NUTS II de 2013. Os pesos são rácios de despesas médias de cada grupo. Diferenças regionais pequenas devem ser interpretadas com cautela.
- A despesa em educação no Alentejo está indisponível. A limpeza preserva os valores em falta e sinaliza as estimativas de baixa fiabilidade identificadas pelo INE.

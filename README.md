# Análise de Vendas — Distribuidora de Livros

Projeto de portfólio para praticar limpeza, tratamento e análise exploratória de dados com **Python (pandas)**. A base simula o histórico de vendas de uma distribuidora de livros, extraída de um sistema antigo sem nenhum tratamento prévio.

## Contexto

O time comercial de uma distribuidora fictícia passou o histórico de vendas dos últimos meses (625 registros) diretamente de um sistema legado. Os dados chegaram com problemas comuns de bases reais: formatos de data inconsistentes, preços em texto (com `R$` e vírgula), nomes de cidade/categoria escritos de formas diferentes, quantidades negativas por erro de digitação, valores ausentes e linhas duplicadas.

O objetivo foi limpar essa base e responder perguntas de negócio que ajudassem a entender o comportamento de vendas.

## Tecnologias

- Python
- pandas / numpy
- matplotlib

## Tratamento realizado

- **Padronização de texto:** colunas de livro, autor, categoria, cidade e forma de pagamento foram normalizadas (remoção de espaços, acentos e capitalização inconsistente).
- **Correção de tipos:** `data_venda` convertida para o tipo data (aceitando os 3 formatos diferentes que vinham na base); `preco_unitario` convertido de texto (com `R$`/vírgula) para número.
- **Preços ausentes:** preenchidos com base no preço mais frequente do mesmo livro/autor/categoria, já que o preço costuma se repetir por produto.
- **Quantidades negativas:** corrigidas com valor absoluto (erro de digitação identificado na base).
- **Quantidades ausentes:** **não foram preenchidas com valores inventados.** As 10 linhas com quantidade ausente foram mantidas na base completa, mas excluídas apenas das análises que dependem de quantidade/receita, para não distorcer os números.
- **Avaliação:** valor por extenso ("cinco") convertido para número; ausências marcadas explicitamente como "Sem Avaliação" em vez de removidas.
- **Cidade e categoria:** variações como "RJ", "BH", "S. Paulo" e "Não-Ficção"/"Nao Ficcao" unificadas em um único valor por local/categoria.
- **Duplicados:** 24 linhas duplicadas identificadas e removidas antes de qualquer cálculo — no primeiro teste, elas chegaram a inflar o ticket médio em quase R$ 3,00.

## Principais insights

- **Ticket médio geral:** R$ 127,14
- **Categoria com mais receita:** Não-Ficção (R$ 21.456,09), seguida de Clássico e Ficção
- **Top livro em receita:** *Pai Rico, Pai Pobre* (R$ 7.143,18 / 138 unidades)
- **Cidade que mais compra (em volume):** Curitiba
- **Canal de venda mais forte:** Telefone, seguido de perto por Marketplace e Site — Loja Física ficou atrás
- **Mês de maior receita:** novembro/2025

## Gráficos gerados

- Top 10 livros por receita e por quantidade (barras horizontais, em gráficos separados por escala)
- Receita por categoria (barras)
- Quantidade vendida por cidade (barras)
- Receita por mês (evolução — sazonalidade)
- Quantidade e receita por canal de venda (barras separadas)

## Como rodar

```bash
pip install pandas numpy matplotlib
jupyter notebook ProjetoPandas.ipynb
```

O arquivo `vendas_livros.csv` precisa estar na mesma pasta do notebook.

## Estrutura do repositório

```
├── ProjetoPandas.ipynb     # notebook com todo o tratamento e análise
├── vendas_livros.csv       # base de dados original (bagunçada)
└── README.md
```

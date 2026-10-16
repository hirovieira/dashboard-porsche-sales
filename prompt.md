# Prompts usados

A dashboard foi gerada por um agente de IA (Claude Code, rodando no app desktop do Claude) com a skill de design de front-end, a partir da base já tratada (`dados/base_tratada.csv`). Abaixo, o prompt principal e os refinamentos, na ordem.

## Prompt 1: geração

```
Você é um analista de dados e desenvolvedor front-end.

Contexto: tenho 100 vendas da Porsche nos EUA (arquivo anexo, já tratado), com as colunas
id, data, modelo, familia, ano, preco (US$), km, pagamento, cidade, estado e status de entrega.

Crie uma dashboard em HTML, arquivo único (index.html), com os dados embutidos em JSON
e Chart.js via CDN. Ela precisa responder três perguntas de negócio:

1. Quais famílias de modelo (911, 718, Cayenne, Macan, Panamera, Taycan) trazem mais
   receita, e com que ticket médio? -> barras de receita + linha de ticket médio.
2. Como os clientes pagam, e quanto vale cada forma de pagamento? -> rosca por receita.
3. Em quais estados está a receita? -> barras por estado, top 12, destacando o top 3.

Topo: cartões com total de vendas, receita, ticket médio e % de vendas entregues.
Filtros: família, estado, forma de pagamento e ano do modelo, todos combináveis,
com botão "Limpar". Todo gráfico, cartão e frase de insight muda com os filtros.
Embaixo: tabela com as 8 maiores vendas do recorte.

Visual: referência Porsche. Fundo quase preto, cards grafite, vermelho #d5001c como
destaque e dourado #b8975a como cor secundária. Títulos em Barlow Condensed
maiúscula com espaçamento largo, texto em Inter. Cada card mostra "PERGUNTA N",
a pergunta e uma frase de insight calculada a partir dos dados filtrados.
Responsivo: no celular, cartões em 2 colunas e gráficos empilhados.
Textos em português do Brasil.
```

## Refinamentos

1. **"O título diz 2024, mas a base tem vendas com data em 2026."** O título virou "Porsche | Sales".
2. **"Quando um filtro zera o recorte, os gráficos ficam vazios sem explicação."** Os insights e a tabela passaram a mostrar "Nenhuma venda neste recorte".
3. **"No gráfico de estados, deixe claro quem puxa a receita."** O top 3 ficou em vermelho, o resto em cinza, e o insight passou a dizer quanto o top 3 soma.

## Conferência no console

Depois de gerar, abri o `index.html` no navegador e conferi no console (F12) que não havia erros. Também conferi no console alguns totais contra a planilha:

```js
VENDAS.length                              // 100
VENDAS.reduce((s, v) => s + v.preco, 0)    // 12827800.5  -> $12.83M no cartão
```

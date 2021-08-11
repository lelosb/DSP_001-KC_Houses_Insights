# KC Houses Insights

## O objetivo deste projeto é explorar uma base de dados de vendas de imóveis para obter insights que gerem valor para o negócio

#### Este projeto foi feito por Leandro Santos Barbosa, baseado nos estudos do curso de formação de Python da Comunidade DS¹

# 1. O problema de negócio

Antes de começar o projeto, devemos contextualizar e entender como o negócio funciona e quais as respostas que procuramos. A House Rocket (empresa fictícia) é uma startup que tem como modelo de negócio a compra e a venda de imóveis baseando suas decisões na análise de dados.

Como membros da equipe de dados da empresa, devemos suportar as decisões das lideranças ajudando a encontrar as melhores oportunidades de negócio no mercado de imóveis, maximizando a receita encontrando as melhores oportunidades.

A principal estratégia é comprar boas casas em ótimas localizações com preços baixos e revendê-las posteriormente à preços mais altos. Quanto maior a diferença entre a compra e a venda, maior o lucro da empresa e portanto maior sua receita.

Entretanto, as casas possuem muitos atributos que as tornam mais ou menos atrativas aos compradores e vendedores e a localização e o período do ano também podem influenciar os preços.

Portanto, seu trabalho como Data Scientist é responder as seguinte perguntas:

Quais casas o CEO da House Rocket deveria comprar e por qual preço de compra?
Uma vez a casa em posse da empresa, qual o melhor momento para vendê-las e qual seria o preço da venda?
A House Rocket deveria fazer uma reforma para aumentar o preço da venda? Quais seriam as sugestões de mudanças? Qual o incremento no preço dado por cada opção de reforma?

Esse conjunto de dados contém casas vendidas entre Maio de 2014 e Maio de 2015. Você usará esses dados para desenvolver sua solução.

Coisas para inserir
Tabela dos dados puros
Tabela genérica
numero de casas
tamanho maximo
preços
média de preços por idade de imóveis
Tem que levar em consideração a coluna condition


Ideias para o meu projeto
as funções de mapa podem ser encapsuladas
Dá pra fazer uma tabela resumo com tudo. O maior número de quartos, a maior area, o maior preço por médio quadrado, etc
Mapa de densidade de imóveis
No streamlit colocar graficos de evolução no tempo
O primeiro passo é carregar a base de dados e verificar o se existem dados faltantes. Nessa caso, não temos. Antes de qualquer operação, verificar os tipos dos dados




# 2. Hipóteses de Negócio
Partimos de uma base de dados que contém preços de venda de casas em King County, em Washington. Cada imóvel possui diversas características, como numero de quartos, área da sala de estar, se possui ou não vista para o mar/lago, etc. A partir desse histórico podemos estudar os dados e tentar entender o quanto  as características de um imóvel (tamanho, localização, vista para o mar, etc) influenciam no preço final de venda, ou seja, no lucro da empresa que tem a compra e venda de imóveis como o core do negócio. Seguem algumas hipóteses iniciais:

Casas com muitos quartos são mais caras? Porque? A partir de quantos quartos o preço aumenta? Qual o incremento de preço por cada quarto adicionado?
As casas mais caras estão no centro? Qual a região? Existe alguma coisa na região que tem correlação com valor de venda da casa? Shoppings? Montanhas? Pessoas Famosas?
Quais seriam os melhores negócios? Qual tipo de casa daria mais lucro? Quais casas são?
Quais casas o CEO da House Rocket deveria comprar e por qual preço de compra?
Uma vez a casa em posse da empresa, qual o melhor momento para vendê-las e qual seria o preço da venda?
Casas com preço abaixo da média e condição boa
A House Rocket deveria fazer uma reforma para aumentar o preço da venda? Quais seriam as sugestões de mudanças? Qual o incremento no preço dado por cada opção de reforma?

comparação dos preços de casas semelhantes ao longo do tempo
comparação das mesmas casas vendidas mais de uma vez
Criação de um mapa interativo com a localização das casas identificadas por faixa de preço, para facilitar a consulta 


# 3. Estratégia da Solução

**Step 01. Data Description:**
A base de dados original possui 21613 registros de transações com 21 atributos por imóvel. Foram identificados 353 registros repetidos. Podem se tratar de imóveis vendidos mais de uma vez durante o período, se possuírem datas diferentes. Caso possuam a mesma data, serão removidos

**Step 02. Feature Engineering:**
area - alguns imóveis possuem área construída maior que a área do terreno. Para os cálculos foram filtradas a maior das áreas por imóvel
price_area - Preço/área - para tornar a comaração justa, deve-se levar em consideração sempre o preço por área

**Step 03. Data Filtering:**
Casas com número de quartos igual a 0 foram excluídas (13 imóveis, menos de 0,07% da base de dados)
Casas com número de banheiros igual a 0 foram excluídas (3 imóveis, menos de 0,02% da base de dados)

Sete imóveis possuíam as duas características, então poderiam ser imóveis comerciais. De qualquer forma, decidiu-se por excluí-los

**Step 04. Exploratory Data Analysis:**

**Step 05. Data Preparation:**

**Step 06. Feature Selection:**

**Step 09. Convert Model Performance to Business Values:**

**Step 10. Deploy Modelo to Production:**

# 4. Top 3 Data Insights

**Hypothesis 01:**

**True/False.**

**Hypothesis 02:**

**True/False.**

**Hypothesis 03:**

**True/False.**


# 7. Business Results

# 8. Conclusions

# 9. Lessons Learned

# 10. Next Steps to Improve

# LICENSE

# Referências
1) Comunidade DS: https://sejaumdatascientist.com/
2) Desafio no Kaggle: https://www.kaggle.com/harlfoxem/housesalesprediction

# All Rights Reserved - Comunidade DS 2021

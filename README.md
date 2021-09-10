# KC Houses Insights

> Status: Colocando em produção ⚠️

## Link do projeto em produção (em breve)

![KingCount](https://github.com/lelosb/DSP_001-KC_Houses_Insights/blob/main/reports/figures/king_count.jpeg)

## O objetivo deste projeto é explorar uma base de dados de vendas de imóveis para obter insights que gerem valor para o negócio.

#### Este projeto foi feito por Leandro Santos Barbosa, baseado nos estudos do curso de formação de Python da Comunidade DS¹ sobre um desafio do Kaggle².

# 1. O problema de negócio

  A House Rocket (empresa fictícia) é uma startup que tem como modelo de negócio a compra e venda de imóveis baseando suas decisões na análise de dados. Como membros da equipe de dados da empresa, devemos suportar as decisões das lideranças ajudando a encontrar as melhores oportunidades de negócio, maximizando assim a receita da empresa.
  A principal estratégia é comprar boas casas em ótimas localizações com preços baixos e revendê-las posteriormente à preços mais altos. Quanto maior a diferença entre a compra e a venda, maior o lucro da empresa e portanto maior sua receita. Entretanto, os imóveis disponíveis possuem muitos atributos que podem influenciar nos preços e na atratividade dos mesmos. Dessa forma, nosso desafio como Data Scientists é responder as seguinte perguntas:

1) Quais casas o CEO da House Rocket deveria comprar e por qual preço de compra?
2) Uma vez a casa em posse da empresa, qual o melhor momento para vendê-las e qual seria o preço da venda?
3) A House Rocket deveria fazer uma reforma para aumentar o preço da venda? 

# 2. Hipóteses de Negócio

  Além de responder essas perguntas, o time de analytics tem também que verificar se as hipóteses do time de negócio são verdadeiras ou não.  Seguem as hipóteses levantadas pelo time de negócio:

1) Casas com vista para o mar são mais caras;
2) Casas que não foram renovadas são mais baratas;
3) Existe uma época do ano melhor para na qual mais casas são vendidas;
4) Existe um atributo numérico além da área que possui alta correlação com os preços;
5) A característica qualitativa mais importante para um imóvel é a localização.

# 3. Estratégia da Solução

INSERIR FLUXOGRAMA DA SOLUÇÃO

## Data Description:

  A base de dados disponível para esse problema contém transações imobiliárias realizadas entre Maio de 2014 e Maio de 2015 em King County, em Washington. A base possui 21613 registros de transações com 21 atributos por imóvel. Na imagem abaixo temos os primeiros 5 registros dos banco de dados:
  
 ![raw_data](https://github.com/lelosb/DSP_001-KC_Houses_Insights/blob/main/reports/figures/raw_data_overview.png)
  
 Os atributos dos imóveis são os seguintes:
 
| Atributos	| Significado |
| ---       |  ---        |
|id	        | Identificação do imóvel |
|date|	Data da venda do imóvel|
|price|	Preço que o imóvel foi negociado |
|bedrooms|	Número de quartos|
|bathrooms|	Número de banheiros |
|sqft_living	| Área em sqft (pés quadrados) do interior dos imóveis|
|sqft_lot|	Área em sqft do terreno|
|floors|	Número de andares do imóvel|
|waterfront|	Atributo que indica se o imóvel possui ou não vista para água (0 = não e 1 = sim)|
|view|	Um índice de 0 a 4 que indica a qualidade da vista da propriedade (0 = baixa 4 = alta)|
|condition|	Um índice de 1 a 5 que indica a condição da propriedade (1 = ruim, 5 = ótima|
|grade|	Um índice de 1 a 13 que indica a construção e o design do edifício (1-3 = baixo, 7 = médio e 11-13 = alta)|
|sqft_above	|Área em sqft construída acima do nível do solo|
|sqft_basement|	Área em sqft construída no nível do solo|
|yr_built	|Ano de construção do imóvel|
|yr_renovated|	Ano de reforma do imóvel (0 - não reformado) |
|zipcode	|Um código de identificação da microregião, similar ao CEP brasileiro|
|lat	|Latitude|
|long|	Longitude|
|sqft_livining15|	Área em sqft do espaço interno de habitação dos 15 vizinhos mais próximos|
|sqft_lot15|	Área em sqft dos terrenos dos 15 vizinhos mais próximos|
  
  No processo de análise inicial dos dados foram identificados 177 registros (id's) de imóveis repetidos. Não foram removidos inicialmente pela possibilidade de se tratarem de imóveis vendidos mais de uma vez durante o período. O critério de exclusão adotado foi que os que possuíssem datas e ids iguais seriam excluídos.

## Feature Engineering:

Features derivadas para apoio à análise:

***area*** - alguns imóveis possuem área construída maior que a área do terreno e vice-versa. Para os cálculos foram filtradas a maior das áreas por imóvel.

  ****Atualização****: Essa feature acabou sendo substituída. Utilizando a maior área entre a área construída ('sqft_living') e a área do terreno ('sqft_lot') surgiram problemas de adequação a realidade. O imóvel mais barato custava absurdos US$ 0,16/sqft, e dada a elevada quantidade de imóveis nessa faixa de valor, não poderiam se tratar de outliers. Uma breve pesquisa na internet³ nos mostrou que o valor correto para os anos de 2014/2015 seria algo entre U$90.00 e U$100.00/sqft. Dessa forma. ao invés de criar uma nova feature optou-se por utlizar a área construida para o cálculo, o que trouxe os valores para valores mais próximos da realidade e praticamente eliminou os outliers.

***price_area*** - média de preço por área. Para tornar a comparação justa, deve-se levar em consideração sempre o preço por área

***zipcode_price*** - Preço médio por área por zipcode - preço para comparação entre os imóveis da mesma região

***location*** - uma "graduação" do zipcode mais barato para o mais caro. Utilizada para identicar a correlação do preço com a localização, transformando o zipcode em uma feature numérica.

***trimester*** -  trimestre do ano no qual ocorreu a transação

## Data Filtering:

Foram removidos por irrelevância ou redundancia:
 - 'sqft_living15', 'sqft_lot15', 'sqft_above', 'sqft_basement' e 'sqft_lot';
 - 'sqft_living' foi substituída por 'area' para facilitar a manipulação e entendimento do código;
 - Casas com número de quartos igual a 0 foram excluídas (13 imóveis, menos de 0,07% da base de dados);
 - Casas com número de banheiros igual a 0 foram excluídas (3 imóveis, menos de 0,02% da base de dados);
 - Sete imóveis possuíam as duas características, então poderiam ser imóveis comerciais. De qualquer forma, decidiu-se por excluí-los.
 
Não foi encontrado nenhum 'id' repetido com datas iguais, por isso todos foram mantidos.

## Exploratory Data Analysis:

### Análise Univariada

  Métricas após limpeza e organização dos dados:

![metrics](https://github.com/lelosb/DSP_001-KC_Houses_Insights/blob/main/reports/figures/metrics.png)

 - Após a mudança do cálculo de preço/área, os preços do dataset se ajustaram ao valores encontrados na pesquisa.
 
 Distribuição dos preços/área (US$ / pé quadrado)
 
 ![Distribuição de preço/área](https://github.com/lelosb/DSP_001-KC_Houses_Insights/blob/main/reports/figures/price_area_distribution.png)
 
### Análise Bivariada

- Foi identificada uma grande variação de preço médio entre casas de 4 para 5;
- A maior quantidade de transações ocorreu no segundo trimestre do ano, enquanto a menor quantidade ocorreu no primeiro trimestre

### Análise Multivariada

Pela análise feita, as características com maior influência no preço são mesmo a área e a localização:

![heatmap](https://github.com/lelosb/DSP_001-KC_Houses_Insights/blob/main/reports/figures/corr_heatmap.png)

## Hypothesis Validation

**Hipótese 01: Imóveis com vista para o mar são mais caros**

**Verdadeira**
Casas com vista para o mar/água são aproximadamente 194% mais caras do que as casas que não têm. A hipótese se verifica mesmo quando se compara casas na mesma localidade.

**Hipótese 2: Casas que não foram renovadas são mais baratas**

**Verdadeira**
Casas que não foram renovadas são aproximadamente 23% mais baratas

**Hipótese 3: Existe uma época no ano em que mais casas são vendidas**

**Verdadeira**

A maioria das casas foi negociada no segundo trimestre (31,58%), enquanto o trimestre com menos negociações foi o primeiro (18,98%). 

![](https://github.com/lelosb/DSP_001-KC_Houses_Insights/blob/main/reports/figures/transations_per__yr.png)

**Hipótese 4: Existe um atributo numérico principal além da área responsável pelo preço das casas**

**Falsa**

Conforme é visível no mapa de calor, todas as variáveis têm uma baixa correlação com o preço/área, com exceção da localização.

**Hipótese 4: A localização é o fator que tem maior correlação com o preço final.

**Verdadeira**

  Conforme o esperado, a característica que mais influencia de forma direta no preço são é localização, seguida da área.
  
## Data Insights

Abaixo seguem os insights obtidos ao longo do projeto pelo time de dados:

1) ***Casas abaixo do preço***
  
  Casas com preço abaixo do valor médio da região devem ser compradas e revendidas com lucro.
  
2) ***Casas com condição 4***
  
  Casas com preço igual ou abaixo do valor médio da região e condição igual a 4 devem ser compradas, renovadas para atingir o grau 5 e revendidas com um lucro maior.
  
![price_condition](https://github.com/lelosb/DSP_001-KC_Houses_Insights/blob/main/reports/figures/avg_price_condition_png)
    
3) **Períodos para as transações**

  O melhor período para compra de imóveis é no primeiro trimestre do ano, pois a procura é menor, o que permite negociações mais agressivas. Enquanto o melhor período para a venda é no segundo trimestre, quanto o mercado está mais aquecido.

4) **Casas com condição 1**

  Imóveis nessas condições não valem a pena ser reformadas, pois o preço médio de uma casa em condição 2 é menor do que o preço médio das casas em condição 1.

# 7. Business Results

As listas de imóveis que devem ser comprados e respectivas sugestões de preços encontram-se nos arquivos anexos (pasta 'reports') e também estão disponíveis no app.

**Casas para serem compradas imediatamente**
Foram identificados 9354 imóveis com preço abaixo do valor médio da área. A compra e posterior venda desses imóveis pelo preço médio da região trará uma expectativa de lucro bruto de U$ 971108343,18 (devem ser subtraídos os custos do processo de compra/venda)

**Casas para serem renovadas e posteriormente vendidas**

Foram identificados 2975 imóveis com preço abaixo do valor médio da área e condição igual a 4. A compra, reforma e posterior venda desses imóveis pelo preço médio das casas de padrão 5 trará uma expectativa de lucro bruto de U$ 834411054,54 (devem ser subtraídos os custos da reforma e do processo de compra/venda)

# 8. Conclusions

[Mapa dos imóveis da base](https://htmlpreview.github.io/https://github.com/lelosb/DSP_001-KC_Houses_Insights/blob/main/reports/map_price.html)

# 9. Deploy

 O modelo em produção será um aplicativo no Streamlit hospedado no Heroku. Está em fase de conclusão.
 
# 9. Lessons Learned

# 10. Next Steps to Improve

  Sugestões para melhoria do projeto:
  - Comparação dos preços de casas semelhantes ao longo do tempo;
  - Utilizar um algoritmo de clusterização para encontrar grupos de imóveis;
  - Comparação das mesmas casas vendidas mais de uma vez;
  - Comparar com o preço médio de casas de condição 5 trouxe alguns valores negativos, isso porque algumas casas de condição 4 possuíam preço/área maior do que a média das casas com condição 5. Para evitar isso pode ser válido comparar as casas por região no próximo ciclo;


# Tecnologias utilizadas

 Código:
 - Python (Pandas, Numpy, Seaborn, Geopandas)
 Produção: 
  - Heroku
  - Streamlit

# LICENSE  

[![NPM](https://img.shields.io/npm/l/react)](https://github.com/lelosb/DSP_001-KC_Houses_Insights/blob/main/LICENSE)
 
# Referências
1) Comunidade DS: https://sejaumdatascientist.com/
2) Desafio no Kaggle: https://www.kaggle.com/harlfoxem/housesalesprediction
3) https://www.statista.com/statistics/682549/average-price-per-square-foot-in-new-single-family-houses-usa/

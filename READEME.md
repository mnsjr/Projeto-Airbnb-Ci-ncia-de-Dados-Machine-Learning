# Projeto Airbnb Rio de Janeiro - Ferramenta de Previsão de Preço de Imóvel 

## Contexto

No Airbnb, qualquer pessoa que tenha um quarto ou um imóvel de qualquer tipo (apartamento, casa, chalé, pousada, etc.) pode ofertar o seu imóvel para ser alugado por diária.<br>
<br>
Você cria o seu perfil de host (pessoa que disponibiliza um imóvel para aluguel por diária) e cria o anúncio do seu imóvel.<br>
<br>
Nesse anúncio, o host deve descrever as características do imóvel da forma mais completa possível, de forma a ajudar os locadores/viajantes a escolherem o melhor imóvel para eles (e de forma a tornar o seu anúncio mais atrativo)<br>
<br>
Existem dezenas de personalizações possíveis no seu anúncio, desde quantidade mínima de diária, preço, quantidade de quartos, até regras de cancelamento, taxa extra para hóspedes extras, exigência de verificação de identidade do locador, etc.<br>



## Objetivo

Construir um modelo de previsão de preço que permita uma pessoa comum que possui um imóvel possa saber quanto deve cobrar pela diária do seu imóvel.<br>
<br>
Ou ainda, para o locador comum, dado o imóvel que ele está buscando, ajudar a saber se aquele imóvel está com preço atrativo (abaixo da média para imóveis com as mesmas características) ou não.

## O que temos disponível, inspirações e créditos

As bases de dados foram retiradas do site kaggle: <https://www.kaggle.com/allanbruno/airbnb-rio-de-janeiro>

- As bases de dados são os preços dos imóveis obtidos e suas respectivas características em cada mês.
- Os preços são dados em reais (R$)
- Temos bases de abril de 2018 a maio de 2020, com exceção de junho de 2018 que não possui base de dados

Expectativas Iniciais

- Acredito que a sazonalidade pode ser um fator importante, visto que meses como dezembro costumam ser bem caros no RJ
- A localização do imóvel deve fazer muita diferença no preço, já que no Rio de Janeiro a localização pode mudar completamente as características do lugar (segurança, beleza natural, pontos turísticos)
- Adicionais/Comodidades podem ter um impacto significativo, visto que temos muitos prédios e casas antigos no Rio de Janeiro

Vamos descobrir o quanto esses fatores impactam e se temos outros fatores não tão intuitivos que são extremamente importantes.

O projeto é formado por dois arquivos:
 - Projeto Ciencia de Dados Airbnb Rio
 - Deploy-Projeto-Airbnb
 
*não fiz upçoad das bases de dados no Github pois tem aproximadamente 5gb. 
<https://www.kaggle.com/allanbruno/airbnb-rio-de-janeiro>

## Scikit-learn | Modelos Testados
<https://scikit-learn.org/stable/><br>

Os modelos testados foram os seguintes:<br>
Modelo RandomForest<br>
   R²: 97.24%<br>
 RSME: 44.05<br>

<br>
Modelo LinearRegression<br>
   R²: 32.70%<br>
 RSME: 217.54<br>

<br>
Modelo ExtraTress<br>
   R²: 97.51%<br>
 RSME: 41.84<br>

<br>

## Análise do Melhor Modelo
Modelo exclolhido foi o ExtraTressRegressor:<br>
 - maior acertividade 97,51%<br>
 - menor valor de RSME, margem de erro<br>
 - velocidade de processamento semelhante à de RandomForest<br>

## Conclusão:
Através da tabela de importância das feature gerada pelo modelo, ou seja, o percentual de impacto de cada feature na previsão do modelo, podemos fazer as seguintes suposições:<br>

A localização tem o maior impacto sobre o preço, visto que latitude e longitude, somam pouco mais de 20% na relevância da formação do preço.<br>
O número de quartos vem em segundo lugar com pouco mais de 10% de relevância. Provavelmente indique que quanto mais quartos, maior o imóvel, maior o número de hóspedes, consequentemente, maior o preço.<br>
O número de comodidades oferecidas pelo host ocupa o terceiro lugar na importância para a formação do preço. Pode ser que o número de comodidades eleve o valor do imóvel ou que a descrição detalhada tenha maior impacto ao despertar o interesse dos hóspedes, promovendo uma menor taxa de vacância.<br>
O número extra de hóspedes impacta no preço, provavelmente porque estes imóveis são maiores e talvez haja uma redundância com o número de quartos.<br>
As acomodações, número mínimo de noites, número de banheiros e tipo, casa ou apartamento tem impacto semelhante, pouco menos de 8% cada.<br>
O número de camas aparece com pouco mais de 5% de relevância.<br>
As demais colunas oferecem menor relevância e eventualmente poderão ser removidas e o modelo testado novamente.

Resultado dos modelos no projeto(gráficos).


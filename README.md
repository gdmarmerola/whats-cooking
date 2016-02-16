# whats-cooking

## "What's cooking?" (Kaggle): minha solução

O objetivo deste [desafio](https://www.kaggle.com/) era classificar uma receita entre 20 tipos de culinária diferentes (brasileira, italiana, etc) com base nos ingredientes utilizados. Os datasets de treino e teste contém, respectivamente, 40 mil e 10 mil exemplos de receitas.   

### Código

Nesta competição, para quase todos os experimentos utilizei notebooks, pois assim existe a possibilidade de mesclar código com markdown, tornando a implementação dos experimentos mais clara e organizada.

##### /code
* `base.py`: imports e algumas funções gerais.
* `hyperopt_search_spaces.py`: definição de espaços de busca para otimização de hiperparâmetros.

##### /notebooks

* `json-processing`: processamento do dataset original, criação de dicionário de termos (ingredientes).
* `feature-extraction`: extração de variáveis utilizando 3 métodos diferentes baseados em tf-idf.
* `feature-engineering`: aplicando algumas técnicas de processamento nas variáveis, como stemming.
* `model-selection`: otimização de hiperparâmetros e validação cruzada, experimentos com diversos algoritmos, histórico de submissões.
   
### Descrição

Esta competição se enquadra na categoria de "ensino" mas já é mais sofisticada que a competição do [Titanic](https://www.kaggle.com/c/titanic), por exemplo.
Existem diversas maneiras de se representar a informação neste caso. Podem ser usadas variáveis binárias para indicar a presença de dados ingredientes ou utilizar algum método para atribuir pesos às variáveis (como tf-idf). Também, o problema pode ser visto como um caso de text mining, onde é interessante utilizar técnicas como stemming, combinações de n-grams, entre outros (nos notebooks há diversos scripts para criar dados utilizando diferentes combinações destas técnicas). 

Em razão de restrições de tempo, os modelos criados foram simples. Não utilizei grandes ensembles e treinei somente um modelo para todas as classes ([esta solução](https://github.com/dmcgarry/kaggle_cooking), por exemplo, cria um modelo para cada uma das classes, além de utilizar diferentes tipos de processamento de dados).

Meu principal objetivo foi me familiarizar com o pacote [XGBoost](https://github.com/dmlc/xgboost), um algoritmo bastante robusto e eficiente que vem mostrando resultados expressivos em competições de ciência de dados. De fato, foi com este algoritmo que obtive o melhor resultado. Para validar os modelos e otimizar hiperparâmetros foi utilizada uma busca aleatória ([hyperopt](https://github.com/hyperopt/hyperopt)) com uma validação cruzada estratificada com 5 folds.

A classificação final foi razoável (593rd/1388), dado o tempo que pude dedicar à competição. O resultado foi uma acurácia de 0.78570.

### Dados e variáveis

Algumas curiosidades sobre o dataset (não processado):

* Ingredientes únicos: 6714 
* Receitas únicas: 39774 (treino), 9944 (teste)

#### Ingredientes mais comuns

Top 20 ingredientes:

salt 18049 <br>
olive oil 7972 <br>
onions 7972 <br>
water 7457 <br>
garlic 7380 <br>
sugar 6434 <br>
garlic cloves 6237 <br>
butter 4848 <br>
ground black pepper 4785 <br>
all-purpose flour 4632 <br>
pepper 4438 <br>
vegetable oil 4385 <br>
eggs 3388 <br>
soy sauce 3296 <br>
kosher salt 3113 <br>
green onions 3078 <br>
tomatoes 3058 <br>
large eggs 2948 <br>
carrots 2814 <br>
unsalted butter 2782 

Distribuição dos 250 ingredientes mais frequentes. Poucos ingredientes formam a base da maioria das culinárias!

![](https://github.com/gdmarmerola/whats-cooking/blob/master/figs/ingred-freqs.png)

#### Culinárias mais comuns

italian         7838 <br>
mexican         6438 <br>
southern_us     4320 <br>
indian          3003 <br>
chinese         2673 <br>
french          2646 <br>
cajun_creole    1546 <br>
thai            1539 <br>
japanese        1423 <br>
greek           1175 <br>
spanish          989 <br>
korean           830 <br>
vietnamese       825 <br>
moroccan         821 <br>
british          804 <br>
filipino         755 <br>
irish            667 <br> 
jamaican         526 <br>
russian          489 <br>
brazilian        467 <br>


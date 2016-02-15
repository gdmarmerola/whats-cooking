# whats-cooking

## "What's cooking?" (Kaggle): minha solução

O objetivo deste [desafio](https://www.kaggle.com/) era classificar uma receita entre 20 tipos de culinária diferentes (brasileira, italiana, etc) com base nos ingredientes utilizados. Os datasets de treino e teste contém, respectivamente, 40 mil e 10 mil exemplos de receitas.   

### Código

Nesta competição, para quase todos os experimentos utilizei notebooks, pois assim existe a possibilidade de mesclar código com markdown, tornando a implementação dos experimentos mais clara e organizada.

##### /code
* `base.py`: imports e algumas funções gerais
* `hyperopt_search_spaces.py`: definição de espaços de busca para otimização de hiperparâmetros

##### /notebooks

* `json-processing`: processamento do dataset original, criação de dicionário de termos (ingredientes).
* `feature-extraction`: extração de variáveis utilizando 3 métodos diferentes baseados em tf-idf.
* `feature-engineering`: aplicando algumas técnicas de processamento nas variáveis, como stemming.
* `model-selection`: otimização de hiperparâmetros e validação cruzada, experimentos com diversos algoritmos, histórico de submissões
   
### Descrição

Esta competição se enquadra na categoria de "ensino" mas já é mais sofisticada que a competição do [Titanic](), por exemplo.
Existem diversas maneiras de se representar a informação neste caso. Podem ser usadas variáveis binárias para indicar a presença de dados ingredientes ou utilizar algum método para atribuir pesos às variáveis (como tf-idf). Também, o problema pode ser visto como um caso de text mining, onde é interessante utilizar técnicas como stemming, combinações de n-grams, entre outros (nos notebooks há diversos scripts para criar dados utilizando diferentes combinações destas técnicas). 

Em razão de restrições de tempo, os modelos criados foram simples. Não utilizei grandes ensembles e treinei somente um modelo para todas as classes ([esta solução](), por exemplo, cria um modelo para cada uma das classes, além de utilizar diferentes tipos de processamento de dados).

Meu principal objetivo foi me familiarizar com o pacote [XGBoost](), um algoritmo bastante robusto e eficiente que vem mostrando resultados expressivos em competições de ciência de dados. De fato, foi com este algoritmo que obtive o melhor resultado. Para validar os modelos e otimizar hiperparâmetros foi utilizada uma busca aleatória ([hyperopt]()) com uma validação cruzada estratificada com 5 folds.

### Dados e variáveis

Algumas curiosidades sobre o dataset (não processado):

* Ingredientes únicos: 6714 
* Receitas únicas: 39774 (treino), 9944 (teste)

#### Ingredientes mais comuns

Top 20 ingredientes:

salt 18049 
olive oil 7972
onions 7972
water 7457
garlic 7380
sugar 6434
garlic cloves 6237
butter 4848
ground black pepper 4785
all-purpose flour 4632
pepper 4438
vegetable oil 4385
eggs 3388
soy sauce 3296
kosher salt 3113
green onions 3078
tomatoes 3058
large eggs 2948
carrots 2814
unsalted butter 2782

Distribuição dos 250 ingredientes mais frequentes. Poucos ingredientes formam a base da maioria das culinárias!



#### Culinárias mais comuns

italian         7838
mexican         6438
southern_us     4320
indian          3003
chinese         2673
french          2646
cajun_creole    1546
thai            1539
japanese        1423
greek           1175
spanish          989
korean           830
vietnamese       825
moroccan         821
british          804
filipino         755
irish            667
jamaican         526
russian          489
brazilian        467


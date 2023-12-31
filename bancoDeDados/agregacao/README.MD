
# [`VIDEO` SQL: Funções de agregação](VIDEO/SQL_Funcoes.de.agregacao.mp4)

Uma função de agregação processa um conjunto de valores contidos em uma única coluna de uma tabela e retorna um único valor como resultado.  
Sua sintaxe é semelhante aquela encontrada em muitas linguagens de programação.  
Contudo, o parâmetro informado é sempre a coluna cujos valores desejamos processar.  

Podemos informar na listagem de colunas do comando `SELECT` uma ou mais funções de agregação, de acordo com a necessidade:  

    SELECT
      funções de agregação(coluna(s))
    FROM
      tabela(s)

Tabelas de exemplo
Para acompanhar os exemplos apresentados nessa documentação, considere a Tabela 1.  

<img src = "img/tabela.png">

***

## MAX  

A função `MAX` analisa um conjunto de valores e retorna o maior entre eles. No exemplo abaixo utilizamos essa função para encontrar o preço de venda mais alto:


    SELECT
      max(precovenda)
    FROM
      produtos

Ao final da execução desse comando será retornado o valor 14.00, como mostra a Figura 1.  

<img src = "img/fun_max.png">

***

## MIN  

`MIN` analisa um grupo de valores e retorna o menor entre eles. A seguir utilizamos essa função para conhecer o preço de venda mais baixo:


    SELECT
      min(precovenda)
    FROM
      produtos


Como retorno para esse comando, obteremos o valor 1.00 conforme mostra a Figura 2.

<img src = "img/fun_min.png">

***

## SUM  

A função `SUM` realiza a soma dos valores em uma única coluna e retorna esse resultado. Para somar todos os preços de venda dos produtos de uma categoria, podemos utilizar essa função informando a coluna PrecoVenda, como exemplificado a seguir:

    SELECT
      sum(precovenda)
    FROM
      produtos
    WHERE
      categoria = 1


Ao final da execução desse comando, teremos o valor 6.65, como mostra a Figura 3.  

<img src = "img/fun_sum.png">  

*Por padrão, a função SUM ignora valores do tipo null.*

***

## AVG  

Com a função `AVG` podemos calcular a média aritmética dos valores em uma única coluna. Usamos essa função no exemplo a seguir, tomando como parâmetro a coluna PrecoVenda da tabela produtos.


    SELECT
      avg(precovenda)
    FROM
      produtos


Ao final da execução desse comando teremos o valor aproximado 5.41, com mostra a Figura 4.  

<img src = "img/fun_avg.png">  

*Por padrão a função AVG ignora valores do tipo null.* 

***

## COUNT  

A função `COUNT` retorna o total de linhas selecionadas. Ela pode receber por parâmetro o nome da coluna ou um asterisco. Por padrão, quando informado o nome de uma coluna, valores do tipo null são ignorados, mas quando informado `*` todas as linhas serão contabilizadas.

Para sabermos o total de produtos em uma categoria, podemos escrever uma consulta como esta:

    SELECT
      count(precovenda)
    FROM
      produtos
    WHERE
      categoria = 1
    

***

## GROUP BY  

Ao utilizar a cláusula `GROUP BY` dividimos os registros que serão agregados em grupos de valores. Essa mudança faz com que tenhamos mais de uma linha como resultado, pois o processamento será realizado uma vez sobre cada um desses grupos.

Para sabermos o produto com maior valor de venda de cada categoria, podemos escrever uma consulta como esta:

    SELECT
      categoria,
      max(precovenda)
    FROM
      produtos
    GROUP BY categoria


Considerando a tabela de produtos, quando essa consulta for executada os dados serão divididos em dois grupos, um para cada categoria, como podemos observar nas Figuras 5 e 6. 


<img src = "img/fun_group1.png">  

Figura 5. Resultado com a função GROUP BY da categoria 1

<img src = "img/fun_group2.png">  

Figura 6. Resultado com a função GROUP BY da categoria 2



Logo após, a função `MAX` será aplicada uma vez para cada um desses grupos, fazendo com que tenhamos como resultado os seguintes valores apresentados na Figura 7.

<img src = "img/fun_group3.png">  

Note que o primeiro registro se refere aos produtos com categoria 1, sendo o segundo o valor máximo dentre os preços de venda dos produtos de categoria 2.

***

## HAVING  

Podemos usar a cláusula `HAVING` em conjunto com `GROUP BY` para filtrar os resultado que serão submetidos a agregação.  

Vemos um exemplo desse filtro na consulta abaixo, que lista o maior preço de venda de cada categoria, incluindo apenas os produtos com preço de venda maior que 10:

    SELECT
      categoria,
      max(precovenda)
    FROM
      produtos
    GROUP BY categoria
      HAVING max(precovenda) > 10


Ao final dessa consulta obtemos os valores apresentados na Figura 8. 

<img src = "img/fun_having.png">  

***

## ALIAS  

A fim de facilitar a compreensão do SQL, podemos utilizar a palavra-chave `as` para criar um apelido para uma coluna. Uma vez que as funções de agregação são retornadas como tal, também podemos fazer uso desse recurso como exemplificado a seguir:

    SELECT
      categoria,
      max(precovenda) as maximo_preco_venda
    FROM
      produtos
    GROUP BY categoria
      HAVING max(precovenda) > 10


Ao final da execução desse código teremos a coluna maximo_preco_venda contendo o maior preço de venda, como mostra a Figura 9.

<img src = "img/fun_alias.png">  

***

## Exemplo prático  

No exemplo a seguir listamos as categorias que contém produtos cujas médias dos preços de custo exceda 2. Para isso agrupamos as categorias com a cláusula `GROUP BY` e filtramos os totais maiores que 2 com `HAVING`:

    SELECT
      categoria,
      avg(precocusto) as media_preco_custo
    FROM
      produtos
    GROUP BY categoria
      HAVING avg(precocusto) > 2


Uma vez que apenas a categoria 2 possui registro que atendem ao filtro estabelecido, receberemos um único registro como resposta, que pode ser observado na Figura 10.

<img src = "img/exemplo.png">   

[CREDITOS](https://www.devmedia.com.br/sql-funcoes-de-agregacao/38463)
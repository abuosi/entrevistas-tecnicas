# entrevistas-tecnicas
Resumo de conhecimento essencial e obrigatório para arrasar em entrevistas técnicas

## Motivação

Praticamente todo processo seletivo de devs tem uma fase de entrevista técnica onde o candidato vai codar ao vivo para demonstrar seu conhecimento.
Por isso é necessário afiar o machado para causar uma boa impressão na entrevista.

Então a grande motivação desse repositório é apresentar o resumo geral desse conhecimento.

Os exemplos aqui são códigos Python válidos, mas os conceitos são aplicavéis a qualquer linguagem de programação.

Então sequem os conhecimentos essencias

## Estrutura de dados lineares

Como as entrevistas técnicas costumam durar apenas uma hora, é raro cairem questões envolvendo estruturas de complexas,
como árvores e grafos. Por isso você deve focar no conhecimento profundo de estruturas de dados lineares. São elas:

1. Lista (List) ou Vetor (Vector)
2. Lista Duplamente Ligada (Double Linked List - Dequeue)
3. Conjunto (Set)
4. Dicionário (Dict) ou Mapa (Map)

A primeira camada é saber quais problemas podem ser resolvidos com essas estruturas de forma simples e eficiente.
Mais importante ainda saber quando não utilizar essas estruturas.
Segue resumo de cada uma:

### Lista (List) ou Vetor (Vector)

São estruturas de dados contíguas extremamente eficientes para leitura de dados por índice. 
Também são extremamente eficientes para adição e remoção de elementos em seu final, sendo excelente implementações de pilhas.
Costumam ser muito utilizadas em problemas que envolvem ordenação de dados, de forma direta ou indireta.
E ainda são eficiente para se obter o tamanho de uma lista e também para trocar um elemento por outro.
Seguem então as operações eficientes:

```python

>>> lista = list(range(1, 10))  # Criação da lista
>>> lista # Lista com 9 elementos contíguos
[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> lista[0] # Acesso eficiente a primeiro elemento
1
>>> lista[1] # Acesso eficiente a segundo elemento
2
>>> lista[-1] # Acesso eficiente ao último elemento
9
>>> lista.append(10) # Adicionando elemento 10 ao final de forma eficiente
>>> lista # Confira elemento adicionado ao final
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
>>> lista.pop() # Removendo último elemento de forma eficiente, inclusive tem nome pop, igual ao definido para uma pilha
10
>>> lista # Confira elemento removido do final
[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> len(lista) # Obtendo tamanho da lista
9
>>> lista[1] = -1 # Alterando segundo elemento de forma eficiente
>>> lista # Confira novo segundo elemento
[1, -1, 3, 4, 5, 6, 7, 8, 9]

```

#### Quando não utilizar Lista (List) ou Vetor (Vector)

Essas estruturas são ineficientes para inserções de elementos em seu início ou meio.
Por isso não devem ser usados em problemas que precisam de filas.
Exemplo de operações ineficientes:

```python
>>> lista = list(range(1, 10))  # Criação da lista
>>> lista # Lista com 9 elementos contíguos
[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> lista.pop(0) # Removendo primeiro elemento de forma ineficiente, quanto maior a lista, mais tempo demora
1
>>> lista # Lista com primeiro elemento removido
[2, 3, 4, 5, 6, 7, 8, 9]
>>> lista.pop(3) # Removendo elemento no meio de forma ineficiente, quanto maior a lista, mais tempo demora
5
>>> lista # Lista com primeiro elemento removido
[2, 3, 4, 6, 7, 8, 9]
>>> lista.insert(0, 1) # Inserindo elemento no início de forma ineficiente, quanto maior a lista, mais tempo demora
>>> lista # Lista com primeiro elemento inserido
[1, 2, 3, 4, 6, 7, 8, 9]

```

Então, para os casos em que se precisa de uma fila, melhor usar uma lista duplamente ligada. Confira na próxima seção.

### Lista Duplamente Ligada (Double Linked List - Dequeue)

São estruturas parecidas com a lista. Mas permitem remoção e inserção eficiente tanto no inĩ́cio quando em fim. 
Por isso são recomendadas em problemas que exigem fila. Confira as operações iguais as das lista que são eficientes:

```python
>>> from collections import deque
>>> lista = deque(range(1, 10))  # Criação da lista
>>> lista # Lista com 9 elementos contíguos
deque([1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> lista.popleft() # Removendo primeiro elemento de forma ineficiente, quanto maior a lista, mais tempo demora
1
>>> lista # Lista com primeiro elemento removido
deque([2, 3, 4, 5, 6, 7, 8, 9])
>>> lista.appendleft(1) # Inserindo elemento no início de forma ineficiente, quanto maior a lista, mais tempo demora
>>> lista # Lista com primeiro elemento inserido
deque([1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> lista.pop() # Também eficiente para remoção do fim da lista
9
>>> lista # Lista com último elemento removido
deque([1, 2, 3, 4, 5, 6, 7, 8])
>>> lista.append(9) # Também eficiente para inserção no fim da lista
>>> lista # Lista com último elemento adicionado
deque([1, 2, 3, 4, 5, 6, 7, 8, 9])

```

#### Quando Lista Duplamente Ligada (Double Linked List - Dequeue)
A lista duplamente ligada não é eficiente para acesso a elementos próximos ao seu meio. Para esses casos, melhor usar listas.

```python
>>> from collections import deque
>>> lista = deque(range(1, 10))  # Criação da lista
>>> lista[4] # Acesso a elemento do meio de forma ineficiente. Quando maior a lista, mais tempo demora
5

```

Por fim, existe uma operação ineficiente para listas duplamente ligadas e listas comuns, confira a seguir.

#### Quando não usar Lista comum ou Duplamente Ligada

Ambas listas, a comum e a duplamente ligada, são ineficientes para a operação de pertencimento. 
Ou seja, para chegar se um elemento está contido nela ou não. Confira a seguir:

```python
>>> from collections import deque
>>> d = deque(range(1, 10))  # Criação da lista duplamente ligada
>>> d # Lista com 9 elementos contíguos
deque([1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> 9 in d # operação ineficiente de elemento que está contido na lista
True
>>> 10 in d # operação ineficiente de elemento que não está contido na lista
False
>>> lista = list(d)  # Criação da lista simples
>>> lista # Lista com 9 elementos contíguos
[1, 2, 3, 4, 5, 6, 7, 8, 9]
>>> 9 in lista # operação ineficiente de elemento que está contido na lista
True
>>> 10 in lista # operação ineficiente de elemento que não está contido na lista
False

```

É muito comum existirem problemas onde é necessário manter a memória de passos já realizados. Para esses casos, deve se
evitar usar listas. Nesse caso, melhor usar conjuntos, confira a seguir.

### Conjunto (Set)

Conjuntos, também chamados de hash sets em algumas liguagens, são muito eficientes para remoção e adição de elementos.
São também extremamente rápidos para operação de pertencimento de elementos.
Eles são parecidos com os conjuntos estudados em matemática e por isso não permitem elementos repetidos. 
Confira as operações eficientes:

```python
>>> conjunto = set() # Criação de conjunto vazio
>>> conjunto
set()
>>> 1 in conjunto # Operação de pertencimento é eficiente
False
>>> conjunto.add(1) # Adição de elementos é eficiente
>>> conjunto
{1}
>>> 1 in conjunto
True
>>> conjunto.update(range(10)) # Adiição de múltiplos elementos é eficiente e não permite duplicatas, só possui 1 uma vez
>>> conjunto
{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
>>> conjunto.add(1)  # Mesmo com adição de elemento, não permite repetição
>>> conjunto
{0, 1, 2, 3, 4, 5, 6, 7, 8, 9}
>>> 1 in conjunto
True
>>> conjunto.remove(1) # Eficiente para remoção de elementos
>>> conjunto
{0, 2, 3, 4, 5, 6, 7, 8, 9}

```

Apesar de conjuntos serem exclentes para se manter backtracking, não permitem acesso a elementos por índices.

#### Quando não usar conjuntos

Conjuntos não são ordenados em muitas linguagens. Por isso não permite acesso por índice. 
Por isso devem ser evitados em problemas de acesso a elementos contíguos ou com ordenação. Confira:

```python
>>> conjunto =set(range(5))
>>> conjunto
{0, 1, 2, 3, 4}
>>> conjunto[0] # Não permite acesso por índice
Traceback (most recent call last):
  ...
TypeError: 'set' object is not subscriptable
>>> for elemento in conjunto: print(elemento) # Mas é possível iterar sobre os elementos
0
1
2
3
4

```

Algumas vezes precisamos conectar elementos a respectivos valores e o conjunto não resolve esse problema. 
Para esse caso devemos usar dicionários, confira a seguir.

### Dicionário (Dict) ou Mapa (Map)

Dicionários, também chamados de mapas ou hash maps, servem para conectar elementos únicos (chaves) a valores.
Em termos de eficiencia de operações, funcionam exatamente como conjuntos, confira a seguir:

```python
>>> frutas ={'banana': 12.50, 'laranja': 1.50, 'uva': 1.20} # Criação de dicionário
>>> frutas['banana'] # Acesso a elemento de forma eficiente, retornando respectivo preço
12.5
>>> frutas['laranja']
1.5
>>> frutas['uva']
1.2
>>> frutas['abacaxi'] = 2.50 # Adicionando elemento de forma eficiente
>>> frutas
{'banana': 12.5, 'laranja': 1.5, 'uva': 1.2, 'abacaxi': 2.5}
>>> frutas['abacaxi'] = 3.75 # alterando valor de forma eficiente
>>> frutas
{'banana': 12.5, 'laranja': 1.5, 'uva': 1.2, 'abacaxi': 3.75}
>>> del frutas['abacaxi'] # Removendo elemento de forma eficiente}
>>> frutas
{'banana': 12.5, 'laranja': 1.5, 'uva': 1.2}

```
Como são parecidos com conjuntos, os casos onde dicionários não devem ser usados são parecidos, confira a seguir.

#### Quando não usar dicionários

Dicionários não são ordenados em muitas linguagens. Por isso não permite acesso por índice. 
Por isso devem ser evitados em problemas de acesso a elementos contíguos ou com ordenação. Confira:

```python
>>> frutas ={'banana': 12.50, 'laranja': 1.50, 'uva': 1.20}
>>> frutas[0] # Não é possível acessar por índice, retorna erro
Traceback (most recent call last):
  ...
KeyError: 0
>>> for nome in frutas: print(nome) # Mas é possível iterar por chaves de forma eficiente
banana
laranja
uva
>>> for preco in frutas.values(): print(preco) # Também possível iterar por valores de forma eficiente
12.5
1.5
1.2
>>> for nome,preco in frutas.items(): print(nome, preco) # Também útil iterar por chave e valor de forma eficiente
banana 12.5
laranja 1.5
uva 1.2

```

Assim se encerram as estruturas de dados lineares necessárias para se resolver 99% das questões de entrevistas técnicas.

### Conclusão sobre estruturas de dados lineares

Conhecer as quatro estruturas de dados lineares elementares é fundamental para passar na entrevista técnicas de processos seletivos para devs.
Saber escolher a estrutura de dados mais adequada para um problema é essencial para demostrar conhecimento dos fundamentos.
E esse conhecimento já deve fazer o profissional passar em várias entrevistas para empresas médias e pequenas.

Agora se você pretende trabalhar em grandes empresas, principalmente as do exterior e ou americanas, como Google e Facebook, você vai precisar ir além.
Você vai precisar conhecer e analisar seus algorítmos do ponto de vista de complexidade em tempo de execução e memória.
Veja o resumo desse assunto na próxima seção.

## Análise e Complexidade de Algoritmos

Análise de complexidade de tempo de execução e uso de memória é uma matéria de faculdade que muitas vezes só e visa na pós graduação, no Brasil.
Contudo essa matéria é dada na graduação das faculdades americanas e saber fazer essa análise é indipensável para quem quer fazer processos seletivos de empresas grande, como Google e Facebook.

Você não precisa ter um conhecimento profundo, mas precisa conseguir fazer essa análise de rapidamente e visualmente na hora do processo seletivo.

Além disso, precisa saber usar a análise para tentar buscar soluções eficientes. 
A heurística que funciona é:

1. Valide que entendeu os requistos dos problemas, incluindo natureza de entradas e saídas dos programas
2. Faça a solução mais simples possível, mesmo que ineficiente. Não resolver é pior que implementar solução ineficiente.
3. Analise a complexidade da solução
4. Verifique como melhorar a perfomance, como por exemplo, ordenar as entradas do programa.
5. Impĺemente a melhora de perfomance proposta.

Então, para poder fazer essa análise e heurística, você precisa:

1. Saber as 7 principais funções de análise e complexidade
2. Saber comparar cada uma dessas funções em termos de peformance
3. Saber a complexidade das operações das estruturas lineares
4. Conhecer e saber a complexidade dos algorítmos clássicos de soluções de problemas

Vamos então detalhar cada um desses pontos.

### As 7 funções de análise e complexidade de algorítmos

Em análise e complexidade de algorítmos usando se usa a notação [Big O](https://en.wikipedia.org/wiki/Big_O_notation) para expressar a evolução do tempo de execução e uso de memória de algoritmos.
Você só precisa conhecer 7 dessas funções

#### 1. O(1) - Constante

ALgorítmos de tempo de constante são aqueles em que tempo de execução e memória independem do tamnho da entrada.
Ou seja, mesmo para uma lista grande de elementos, o algorítmo vai demorar sempre o mesmo tempo para executar.
Esse tipo de algorítmo é o mais eficiente que existe, mas normalmente apenas problemas muito simples permitem solução constante.
Segue uma tabela com as principais operações de tempo constante:

| Categoria             | Operação | Descrição | Exemplo                             |
|-----------------------|----------|-----------|-------------------------------------|
| **Operações Básicas** | Atribuição de variável | Armazenar valor em variável | `x = 5`                             |
| **Operações Básicas** | Operações aritméticas | Soma, subtração, multiplicação, divisão | `a + b`, `x - y`, `m * n`, `p / q`  |
| **Operações Básicas** | Operações lógicas | AND, OR, NOT, comparações | `a and b`, `x > y`, `not flag`      |
| **Operações Básicas** | Acesso a atributo | Acessar propriedade de objeto | `obj.propriedade`                   |
| **Lista (List)**      | Acesso por índice | Ler elemento em posição específica | `lista[0]`, `lista[5]`, `lista[-1]` |
| **Lista (List)**      | Modificação por índice | Alterar elemento em posição específica | `lista[1] = -1`                     |
| **Lista (List)**      | Adicionar ao final | Inserir elemento no fim da lista | `lista.append(10)`                  |
| **Lista (List)**      | Remover do final | Retirar último elemento | `lista.pop()`                       |
| **Lista (List)**      | Obter tamanho | Quantidade de elementos | `len(lista)`                        |
| **Deque**             | Adicionar ao final | Inserir elemento no fim | `deque.append(9)`                   |
| **Deque**             | Remover do final | Retirar último elemento | `deque.pop()`                       |
| **Deque**             | Adicionar ao início | Inserir elemento no começo | `deque.appendleft(1)`               |
| **Deque**             | Remover do início | Retirar primeiro elemento | `deque.popleft()`                   |
| **Deque**             | Obter tamanho  | Quantidade de elementos | `len(deque)`                        |
| **Set**               | Adicionar elemento | Inserir novo elemento | `conjunto.add(1)`                   |
| **Set**               | Remover elemento | Retirar elemento específico | `conjunto.remove(1)`                |
| **Set**               | Verificar pertencimento | Checar se elemento existe | `1 in conjunto`                     |
| **Set**               | Obter tamanho  | Quantidade de elementos | `len(conjunto)`                     |
| **Dict**              | Acesso por chave | Obter valor associado à chave | `dict['chave']`                     |
| **Dict**              | Modificação por chave | Alterar valor de chave existente | `dict['chave'] = novo_valor`        |
| **Dict**              | Adicionar par chave-valor | Inserir nova entrada | `dict['nova_chave'] = valor`        |
| **Dict**              | Remover por chave | Excluir entrada específica | `del dict['chave']`                 |
| **Dict**              | Verificar existência de chave | Checar se chave existe | `'chave' in dict`                   |
| **Dict**              | Obter tamanho  | Quantidade de elementos | `len(dct)`                          |

Portanto você deverá ser capaz de identificar as operações de tempo constante de seu algoritmo e procurar usar as estruturas de dados lineares mais adequadas, buscando operações constantes sempre que possível.
Quando não for possível, procurar usar a próxima solução mais eficinte, que é a logarítimica. Confira a seguir

#### 2. O(log n) - Logarítmico

Os algorítmos logarítimcos são os mais eficientes depois dos constantes. 
Normalmente são logarítimocos os algorítmos que conseguem dividir a entrada em duas partes e, a partir de uma condição, eliminar uma das metades como possível solução.
O mais clássico algoritimo em complexidade logaritímica é a [Busca Binária](https://en.wikipedia.org/wiki/Binary_search).

Conhecer esse algorítmo é importante para poder buscar soluções com eficiencia e até validar com o entrevistador se as condições para usar o algoritmo estão presentes.
Por exemplo, se a entrada for uma lista de números, você pode perguntar se ela está ordenada para já poder efetuar uma busca binária.
Você pode ser pedido para implementar o algoritmo de busca binária. 
Ou então pode usar implementação da linguagem que estiver usando, pois a maioria vai oferecer a solução pronta.
E aí vc vai considerar a complexidade log n do algorítmo.

Exemplo em Python

```python
>>> from bisect import bisect_left, bisect_right
>>> lista= list(range(1, 20, 3))
>>> lista
[1, 4, 7, 10, 13, 16, 19]
>>> bisect_left(lista, 10) # onde inserir o 10, na posição mais a esquerda, para manter a lista ordenada, custo O(log n)
3
>>> bisect_right(lista, 10) # onde inserir o 10, na posição mais a direita, para manter a lista ordenada, custo O(log n)
4

```





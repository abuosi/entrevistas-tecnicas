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
3. Dicionário (Dict) ou Mapa (Map)
4. Conjunto (Set)

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

### Quando não usar Lista comum ou Duplamente Ligada

Ambos listas, a comum e a duplamente ligada, são ineficiente para a operação de pertencimento. 
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

É muito comum existerem problemas onde é necessário manter a memória de passos já realizados. Para esses casos, deve se
evitar usar listas. Nesse caso, melhor usar conjuntos, confira a seguir



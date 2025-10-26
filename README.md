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
Você vai precisar conhecer e análisar seus algorítmos do ponto de vista de complexidade em tempo de execução e memória.
Veja o resumo desse assunto na próxima seção.



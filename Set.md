# SET
> link: https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_methods_system_set.htm

> É um conjunto, uma coleção de elementos que NÃO TEM DUPLICATAS e é não ordenada, ou seja, NÃO TEM ÍNDICE (essas são as diferenças pra listas).
>> É interessante trabalhar com SET para ID, porque não pode ter ID duplicado.

## Criar SET
```
Set<String> testeSet = new Set<String>();
```
```
Set<String> nomeSet = new Set<String>{'João', 'Maria', 'Antonio'};
System.debug('Valor do SET: ' + nomeSet);

-> Valor do SET: {Antonio, João, Maria} //ordena em ordem alfabética.
```
```
Set<Integer> inteiros = new Set<Integer>{1, 8, 3, 5, 6, 8, 8};
System.debug('Valor do SET: ' + inteiros);

-> Valor do SET: {1, 3, 5, 6, 8} //ordem crescente e não mostra duplicatas.
```
## método add() - Adiciona valores no SET 
```
Set<String> nomeSet = new Set<String>{'João', 'Maria', 'Antonio'};

nomeSet.add('Carlos');
System.debug('Valor do SET: ' + nomeSet);

-> Valor do SET: {Antonio, Carlos, João, Maria} //ordena de forma alfabética
```

## método contains() - verifica se o set contem ou não determinado item
```
nomeSet.contains('Maria');
```

## método remove() - deleta um item, porém não pelo índice e sim pelo valor
```
nomeSet.remove('Maria');
```

## método clear() - remove todos os itens
```
nomeSet.clear();
```

## método size() - retorna o tamanho do SET
```
System.debug(nomeSet.size());
```

## método isEmpty() - checa se o SET é vazio
```
System.debug(nomeSet.isEmpty());
```
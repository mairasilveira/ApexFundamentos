# ARRAY
> link:

*Uma lista ou um array do Apex é um grupo ordenado de itens do mesmo tipo, como uma lista de compras. As variáveis armazenam um dado só (ex: String nomes = 'Maria';), o array armazena vários.*

## Criação de array chamado nomes do tipo string com 4 índices (0 1 2 3):
```
STRING[] nomes = new STRING[4];
System.debug('Valor do array: ' + nomes);

-> Valor do array: (null, null, null, null)
```

## Criação de array com duas strings
```
STRING[] nomes = new STRING[]{'José', 'Maria'};
System.debug('Valor do array: ' + nomes);

-> Valor do array: (José, Maria)
```

## Atribuir valores por índice:
```
STRING[] nomes = new STRING[4];
nomes[1] = 'José';
nomes[3] = 'Marira';
System.debug('Valor do array: ' + nomes);

-> Valor do array: (null, José, null, Marira)
System.debug('Valor do índice 3: ' + nomes[3]);
-> Valor do índice 3: Marira
```

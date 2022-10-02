# SET
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

## método get()
*retorna valores do SET*

# MAP
> Um mapa é uma coleção de pares de valores - chave em que cada chave exclusiva é mapeada para um único valor.
>> Map<chave, valor> ex. chave=USA, valor=dólar

## Criar MAP
```
Map<String, String> moedasPais = new Map<String, String>();
```
```
Map<Integer, String> mapNomes = new Map<Integer, String>();
```

## métodos get() e put() - Retornar valores e Adicionar valores dentro do map
```
mapNomes.put(1, 'João');
mapNomes.put(2, 'Maria');
mapNomes.put(3, 'Cata');

System.debug('Valor do map: ' + mapNomes.get(2)); //o método get() retorna valores do map

-> Valor do map: Maria
```

## método isEmpty() - Verifica se a coleção está vazia
```
if(mapImoveis.isEmpty()){
	System.debug('Mapa está vazio');
	}else{
	System.debug('Não está vazio');
	}
```

## Utilidades do map no Salesforce
```
Map<Id, Imoveis__c> mapImoveis = new Map<Id, Imoveis__c>([SELECT Id, Valor__c FROM Imoveis__c LIMIT 10]);

//mostrar os IDS do map
//cria for para percorrer somente as chaves (primeiro item de cada par do map) do mapImoveis usando keySet()
for(Id idChave : mapImoveis.keySet()){
	Imoveis__c imv = mapImoveis.get(idChave);
	System.debug('Imóveis por ID: ' + imv);
	}

-> Imóveis por ID: Imoveis__c:{Id=a026g00000DvSBbAAM, Valor__c=4500}
   Imóveis por ID: Imoveis__c:{Id=a026g00000DumV6AAJ, Valor__c=2000}
```


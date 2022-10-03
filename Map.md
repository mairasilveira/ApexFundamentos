# MAP
> Um mapa é uma coleção de pares de valores - chave (cada chave é exclusiva e mapeada para um único valor) e valores.
>> Chave não pode ter duplicata (igual SET), valor pode ter duplicata (igual List)
>>> Um item é acessado através da chave

Map<chave, valor> ex. chave=USA, valor=dólar

## Exemplo
```
Map<Integer, String> class2022 = new Map<Integer, String>();

class2022.put(11008890, 'Joana');
class2022.put(11008100, 'Maíra');
class2022.put(11008100, 'Joana');
```

| Keys | 11008890     | 11008100| 11008100|
|-----------| ----------- | ----------- | ----------- |
| Values | Joana     | Maíra       |   Joana |

## Criar MAP
```
Map<String, String> moedasPais = new Map<String, String>();
```
```
Map<Integer, String> mapNomes = new Map<Integer, String>();
```
> Maps podem obter coleção como valores
>> Exemplo. se um artigo pode ter vários posts em cada:
```
 Map<String, List<String>> todosPosts = new Map<String, List<String>>();

 // onde cada list armazena os títulos dos posts
 List<String> apexPosts = new List<String>{'salesforce', 'poo'};
 List<String> javascriptPosts = new List<String>{'frontend', 'HTML'};

 // inserir os posts
 todosPosts.put('Apex', apexPosts);
 todosPosts.put('Javascript', javascriptPosts);

 System.debug(todosPosts);

 -> {Apex=(salesforce, poo), Javascript=(frontend, HTML)}

```

## métodos get() e put() - Retornar valores e Adicionar valores dentro do map
```
mapNomes.put(1, 'João');
mapNomes.put(2, 'Maria');
mapNomes.put(3, 'Cata');

System.debug('Valor do map: ' + mapNomes.get(2)); //o método get() retorna valores do map através da chave

-> Valor do map: Maria

Obs. se tentar inserir um item com chave duplicada ele substituirá a chave anterior com o novo valor
```

## método isEmpty() - Verifica se a coleção está vazia
```
if(mapImoveis.isEmpty()){
	System.debug('Mapa está vazio');
	}else{
	System.debug('Não está vazio');
	}
```

## método remove() - remove um item do MAP pela sua chave
```
class2022.remove(11008890);
```

## método containsKey() - Checa se o MAP tem uma chave
```
System.debug(class2022.containsKey(11008890));
```

## método keySet() - Obter todas as keys
```
System.debug(class2022.keySet());
```
```
Set<Integer> rollNumber = class2022.keySet();
System.debug(rollNumber);
```

## método values() - Obter todos os valores
```
class2022.values();
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


# LIST
> link: https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_methods_system_list.htm

*É uma coleção, como o array, mas tem algumas particularidades:*
- Lista também tem índices (0, 1...) porém ao contrário do array nós não podemos definir um tamanho para ela, ela já tem um tamanho máximo que pode ser utilizado.
- Na lista podemos fazer listas por exemplo de registros, de objetos, de leads, de contatos... o tipo da lista de um objeto seria do tipo objeto. No array não conseguimos fazer isto.

### CRIAR LISTAS
```
List<Integer> numeros = new List<Integer>{10, 23, 40};
```
```
List<String> nomes = new List<String>();
System.debug('Valor da lista: ' + nomes);

-> Valor da lista: ()
```
```
List<String> nomes = new List<String>{'José', 'Maria'}; //Note que não tem () quando tem {} com valores in line
System.debug('Valor da lista: ' + nomes);

-> Valor da lista: (José, Maria)
```

### ADICIONAR DADOS NA LISTA
```
nomes.add();
```
```
nomes.add('José'); //método global, adicionou josé em uma posição. Só pode adicionar um valor por vez
nomes.add('Maria');
System.debug('Valor da lista: ' + nomes);

-> Valor da lista: (José, Maria)
```
```
numeros.add(8); //adiciona item na lista (numero 8)
numeros.add(1, 8) //adiciona numero 8 no índice 1
```

### REMOVER ITENS OU LIMPAR TODA A LISTA
```
nomes.remove(); || nomes.clear();
```
```
nomes.remove(1); //remove item do índice 1
```
```
nomes.clear(); //remove todos os itens da lista.
```

### BUSCAR VALORES PELO ÍNDICE
```
nomes.get();
```
```
System.debug('Valor na posição 1: ' + nomes.get(1)); //nomes.get(1) busca o valor no índice 1 da lista
```

### OBTER TAMANHO DA LISTA (NÚMERO DE ITENS)
```
nomes.size();
```

### ATUALIZAR ITEM (SUBSTITUIR VALOR POR OUTRO)
```
nomes.set(índice, valor novo);
```
```
nomes.set(1, 10); //substitui o item do índice 1 pelo numero 10
```

### OBTER TODOS OS ITENS DA LISTA
```
List<Contact> lista = new List<Contact>();

for(Contact var : lista){
	System.debug(var)
}
```
```
List<Account> nomeLista = [SELECT Name, Title FROM Account];

for(Account x : nomeLista){
	System.debug("Nome: " + x.Name + " TItle: " + x.Title);
}
```

# EXEMPLO
## CRIANDO UMA LISTA DO TIPO IMÓVEIS (Sobjects)
```
List<Imoveis__c> imoveis_list = new List<Imoveis__c>();
System.debug('Valor da lista: ' + imoveis_list);

-> Valor da lista: ()
```

## PREENCHENDO A LISTA COM IMÓVEIS
> Operação DML, busca imóveis no banco de dados, usando SOQL e adiciona dentro da lista:
```
imoveis_list = [SELECT id, Valor__c FROM Imoveis__c]; //está pegando o campo valor dentro do objeto imóveis e adicionando na lista
System.debug('Valor da lista: ' + imoveis_list);

-> Valor da lista: (Imoveis__c:{Id=a026g00000DvSBbAAN, Valor__c=4500,000}, Imoveis__c:{Id=a026g00000DumV8AAAK, Valor__c=2200,000})
```

## PERCORRENDO A LISTA E ENCONTRANDO IMÓVEIS DE VALOR ACIMA DE 3000

```
Integer contador = 0;

//Para percorrer a lista precisa de uma variável do tipo Imoveis__c (no caso chamará imv)

for(Imoveis__c imv : imoveis_list){
	if(imv.Valor__c > 3000){
	contador += 1;
	}
}
System.debug('Quantidade de imóveis maiores que 3000: ' + contador);

-> Quantidade de imóveis maiores que 3000: 1
```
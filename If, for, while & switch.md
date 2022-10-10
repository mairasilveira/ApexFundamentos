# CONDICIONAIS

## IF
```
String CNPJ = '51.694.190/001-18';
    	
    if(CNPJ.length() == 18 && CNPJ != 0){
        System.debug('CNPJ Válido');
    }else{
        System.debug('CNPJ Inválido');
    }
```

## TERNÁRIO
## Condição ? (Valor SE Verdadeiro) : (Valor SE Falso)
```
String CNPJ = '51.694.190/001-18';
String CNPJ_Valido = 'Este CNPJ é válido';
String CNPJ_Invalido = 'Este CNPJ é inválido';

String resultado = CNPJ.length() == 18 ? CNPJ_Valido : CNPJ_Invalido;
System.debug('Valor do resultado: ' + resultado);

-> Valor do resultado: Este CNPJ é inválido
```

# LAÇOS OU ESTRUTURAS DE REPETIÇÃO

## FOR
```
integer soma;

for(integer i; i<10; i++){
    soma = i;
    System.debug('Valor da soma: ' + soma);
}
```
## FOR EACH - Itera sobre todos os elementos de uma lista ou SET
> Neste caso percorre a lista teste inteira

```
List<Integer> teste = new List<Integer>{100, 200};

for(Integer num : teste){
	System.debug('número atual = ' + num);
}


->
número atual = 100
número atual = 200
```


## WHILE
```
integer contador = 0;

while(contador < 10){
	System.debug(contador);
	contador++; //contador = contador + 1
}
```

## DO WHILE
```
integer contador = 0;

do{
	System.debug('Valor do contador: ' + contador);
	contador++;
}while(contador < 10);
```

## SWITCH-WHEN

```
String diaDaSemana = 'Domingo';

Switch on diaDaSemana {
	when 'Domingo' {
		System.debug('Dia de almoço na casa da sogra');
	}
	when 'Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta' {
		System.debug('Dia útil');
	}
	//valor default
	when else {
		System.debug('Dia da semana não encontrado');
	}
}
```

## BREAK - Declaração de interrupção
> Utiliza-se a palavra *break* para sair de um loop. Ex:
```
Integer n;
for (Integer i=1; i<=n; i++){
	//procurar número na lista
	if (//achar o número == true){
		break;
	}
}
```

## CONTINUE - Pula a iteração do loop
> Exemplo - para comer frango todos os dias da semana, exceto terça feira:
```
List<String> days = new List<String>{'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday'};

for (Integer i=0; i<days.size(); i++){
	if(days.get(i)=='Tuesday') {
		continue;
	}
	System.debug('It's ' + days.get(i) + '. Eat chicken');
}


-> 
It's Monday. Eat chicken
It's Wednesday. Eat chicken
It's Thursday. Eat chicken
It's Friday. Eat chicken
It's Saturday. Eat chicken
It's Sunday. Eat chicken
```
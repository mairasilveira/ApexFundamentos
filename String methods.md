# STRING METHODS
> link: https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_methods_system_string.htm

*Abaixo seguem alguns métodos para a seguinte variável str:*
```
String str = 'eu sou uma variável de string';
System.debug('Atual String: ' + str);

-> Atual String: eu sou uma variável de string
```
> capitalize() - a primeira letra da string vira letra maiúscula
```
System.debug('Capitalize String: ' + str.capitalize());

-> Capitalize String: Eu sou uma variável de string
```
> contains('palavra') - mostra se a string contém a palavra 'palavra'
```
System.debug('Contém riável?:' + str.contains('riável'));

-> Contém riável?: true
```
> toUpperCase() - converte para maiúscula
```
System.debug('Maiúscula: ' + str.toUpperCase());

-> Maiúscula: EU SOU UMA VARIÁVEL DE STRING
```
> toLowerCase() - converte para minúscula
```
System.debug('Minúscula: ' + str.toLowerCase());

-> Minúscula: eu sou uma variável de string
```
> replace() - substitui parte da string por outra string
```
System.debug('Substituir: ' + str.replace('de string', 'nova');

-> Substituir: eu sou uma variável nova
```
> equals() - diz se uma string é igual a outra
```
System.debug('Is equal to ring?: '+ str.equals('ring'));
```
```
String str1 = 'Manish';
String str2 = 'maNish';

System.debug('str1 equals str2: ' + str1.equals(str2));

-> str1 equals str2: false

System.debug('str1 equals str2 ignore case: ' + str1.toLowerCase().equals(str2.toLowerCase()));

-> str1 equals str2 ignore case: true
```
> remove() - remove caracteres da string
```
System.debug('Remove ring: ' + str.remove('ring'));

-> Remove ring: eu sou uma variável de st
```
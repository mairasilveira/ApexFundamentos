# Tipos primitivos

- String palavra = 'ForceNoob';
- Integer numeros = 0123456789;
- Long numero = 70000000000L;
- Boolean check = true;
- Decimal taxa = 1.95; //também tem Double e Long
- Blob //armazena arquivos, ex: armazena imagem
- Date today = Date.newInstance(2020, 5, 18);
- Time currentTime = Time.newInstance(3, 25, 0, 0);
- DateTime currentDateTime = DateTime.newInstance(2020, 5, 18, 3, 25, 0);
- ID

# Tipos específicos Salesforce

- Id idAccount; //no SF tudo tem um id, cada registro, usuário etc (identificador único que fica no meio da url). É uma string, tem que ser entre aspas ''
- Sobject //É como se fosse "criar uma variável do tipo objeto" Tem que instanciar o objeto - POO
  
## Criando um sObject no salesforce:

```
Imoveis__c casa = new Imoveis__c(); 
```
> Imoveis__c é o nome de API ou nome único do objeto
>> casa é um nome qualquer para a variável
>>> = new Imoveis__c() é pra instanciar o objeto 

*Se escrever o nome da variável e um . vai aparecer os campos do objeto para selecionar. Ex: casa.Quartos__c*
# Anotações

## @deprecated
- Indicação que o pedaço de código está obsoleto.
```
@deprecated
// Este método está obsoleto
// Use play2020() instead
public void play2019(){
}
```
## @AuraEnabled(cacheable=true)
- Disponibiliza o método para ser utilizado dentro lightning.

```
public class AccountController {

@AuraEnabled(cacheable=true)
public static List<Account> getAllAccount() {
    return accounts;
}

}
```
## @Future
- Ajuda a criar métodos futuros

## @InvocableMethod
- O método pode ser chamado a partir dos fluxos visuais
```
public class AnnotationsDemo {

    @InvocableMethod
    public static void method(){
    }

}
```

## @ InvocableVariable

## @IsTest
- Indica que é um teste. Um método de teste PRECISA estar dentro de uma classe de teste, deve ser PUBLIC ou GLOBAL, STATIC e VOID
```
@isTest
public class Myclass {
    @isTest
    public static void myTest(){
    }
}
```
### Assert - método de declaração
> Usado para checar se o código está se comportando conforme o esperado. 
```
System.assert(a == b, 'Error: A is not equal to B');
* Boolean. Se a != b receberemos um erro que o teste falhou


System.assertEquals(a, b, 'A is not equal to);
* a = valor esperado do método, b = o valor obtido do método. Se a != b receberemos um erro que o teste falhou


System.assertNotEquals(a, b);
* a = valor que não pode ser, b = valor obtido do método. Se a = b receberemos um erro que o teste falhou
```

## @ReadOnly

## @RemoteAction

## @TestSetup

## @TestVisible

## @Track
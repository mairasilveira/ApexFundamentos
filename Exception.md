# Exception
> link com os tipos de exceptions: https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_classes_exception_methods.htm

Apex usa exceptions para notificar erros e eventos que fujam do fluxo normal da execução do código.
- Ex. se a operação DML falhar ( ex. insert de contato sem algum campo obrigatório) temos uma exceção DML
- Ex. exceção matemática (ex. dividir um número por 0)
____

## Try_Catch_Finally
> Feito para não interromper o fluxo do código caso haja exceptions
>> O bloco catch só é executado se há a exception definida
>>> O bloco finally sempre será executado, independente de haver exceptions

### EXCEPTION (CAPTURA TODOS OS TIPOS DE EXCEPTION)
```
try{

}catch(Exception e){

}
```
### MATH EXCEPTION
```
try{
        Double result = 10/0;
        System.debug('Result: ' + result);
    } catch(MathException e){
        System.debug('Math exception cought');
    } finally {
        System.debug('finally called');
}
```
### DML EXCEPTION
```
try{
        Account acc = new Account();
        insert acc;
    } catch(DMLException e){
        System.debug('DML exception cought');
    } finally {
        System.debug('finally called');
}
```
# Criar a própria Exception
> Criar nova classe Apex
>> Extender a classe de exceção
>>> Throw: Palavra utilizada para gerar um exception completo ou lançar alguma mensagem personalizada
```
public class ProcessException extends Exception {
    try{
        throw new ProcessException('My custom exception');
    }catch(Exception e){
    System.debug('Linha: ' + e.getLineNumber()); //Retorna o número da linha que teve a exception
    System.debug('Cause: ' + e.getCause()); //Causa do exception
    System.debug('Message: ' + e.getMessage()); //Mensagem de erro
    System.debug('Stack ' + e.getStackTraceString());
    }
}
```

# Exception Methods

Ex. Double result = 10/0 - no caso da MathException essa é a linha
```
try{
    // codigo
} catch(Exception e){
System.debug('Linha: ' + e.getLineNumber()); //Retorna o número da linha que teve a exception
System.debug('Cause: ' + e.getCause()); //Causa do exception
System.debug('Message: ' + e.getMessage()); //Mensagem de erro
System.debug('Stack ' + e.getStackTraceString());
}
```


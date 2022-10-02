# Trigger
> Permitem que você execute ações personalizadas definidas antes ou depois de determinados eventos para registros no Salesforce, tais como: inserções, atualizações ou exclusões.
>> No flow (fluxo) ações poderão ser utilizadas quando um registro for criado, atualizado ou excluído. A trigger/código só será utilizado quando uma personalização da salesforce não for possível.
>>> Na exceução de CREATE e UPDATE a ação pode ser realizada ANTES E DEPOIS, já o DELET a ação é executada antes de ser excluído

| Syntax      | Description |
| ----------- | ----------- |
| Before insert | Ações a serem executadas antes da inserção de uma conta       |
| Before update   | Ações a serem executadas antes da atualização de uma conta        |
| Before delet   | Ações a serem executadas antes de deletar uma conta     |
| After insert  | Ações a serem executadas depois de inserir uma conta       |
| After update  | Ações a serem executadas depois da atualização de uma conta        |
| After delete  | Ações a serem executadas depois de deletar uma conta       |
| After undelete | Ações a serem executadas depois de recuperar conta deletada |
 

## Criar triggle
*Criar -> new apex trigger -> escreve o nome da trigger e seleciona o objeto que você quer referenciar a trigger.
Ex. para um objeto Conta, trigger AccountTrigger*
> Trigger do objeto Imoveis__c que irá definir qual a classificação do imóvel de acordo com seu valor, quando eu crio ou quando atualizo o registro:
```
trigger ImoveisTrigger on Imoveis__c (before insert, before update) {
    
    //se eu tiver atualizando ou criando o registro faça tal coisa
    if(Trigger.isUpdate || Trigger.isInsert){
        
        //percorrer a lista de registros que estão sendo atualizados (Trigger.new)
        for(Imoveis__c imv : Trigger.new){
            if(imv.Valor__c <= 100000){
                imv.Classificacao__c = 'Bronze';
            } if (imv.Valor__c > 100000 && imv.Valor__c <= 350000){
                imv.Classificacao__c = 'Prata';
            } if (imv.Valor__c > 350000) {
                imv.Classificacao__c = 'Ouro';
            }
        }
        
    }
    
}

//Ps. esse exemplo poderia ser resolvido com uma regra de trabalho ou fluxo, não precisa ser feita uma trigger
```

## TriggerHandle
*Quando tem muitas regras de negócios, delega as ações que teriam na trigger para uma classe que as ações podem estar nesta classe ou a classe chama outra classe.*

## Criar TriggerHandle
```
// Passo 1: Criar um novo arquivo de trigger

trigger ImoveisTriggers on Imoveis__c (after insert) {
//se a trigger é depois de inserir faz tal coisa
    if(trigger.isAfter && trigger.isInsert){
        ImoveisTriggerHandler.AtualizaClassificacao(Trigger.new); //Chama o método da classe
    }
    
}

// Passo 2: Criar uma nova classe

public class ImoveisTriggerHandler {
    //Quando este método for chamado ele vai receber como parâmetro uma lista do tipo imóvel - a Trigger.new
    public static void AtualizaClassificacao(List<Imoveis__c> novoImovel){
        List<Imoveis__c> imvAtualizar = [SELECT Id, Valor__c, Classificacao__c FROM Imoveis__c WHERE Id IN :novoImovel];
        
        for(Imoveis__c imv : imvAtualizar){
            if(imv.Valor__c <= 100000){
                imv.Classificacao__c = 'Bronze';
            }
            if(imv.Valor__c > 100000 && <= 350000){
            imv.Classificacao__c = 'Prata';
            }
            if(imv.Valor__c > 350000){
            imv.Classificacao__c = 'Ouro';
    		}
		}
        
        update imvAtualizar; //como este método não está no documento da trigger e sim em uma classe, precisa escrever a operação para atualizar no banco de dados as modificações. Operações: insert, update, delete, upsert
```
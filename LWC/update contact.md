## NO HTML DO LWC
```
<div class="slds-p-around_small">
                <lightning-button onclick={testeUpdateJS} label="Update Contc" value="Update" variant="success"></lightning-button>
            </div>
```

## NO JAVASCRIPT DO LWC
```
import { LightningElement, track, api, wire} from 'lwc';
import testeUpdate from '@salesforce/apex/TesteInsertController.testeUpdate';

 testeUpdateJS(){
        testeUpdate({
        })
        .then(record => {
            window.console.log('update',record)
           })
           .catch(error => {
            window.console.log('error', error)
           })
    }
}
```

*verificar o que precisa colocar no @track*

## NA CLASSE

```
public with sharing class TesteInsertController {
    @AuraEnabled
public static void testeUpdate(){
            try {

//Criar lista para inserir os emails (porque existe mais de um contato chamado francisco). Lembrar do Id no SELECT
                List<Contact> updateContato = new List<Contact>([SELECT Id, Email FROM Contact WHERE FirstName='francisco']);
//For each para percorrer a lista criada e em seguida modificar o campo Email
                for(Contact Contato : updateContato){
                    Contato.Email = 'francisco.targa@crm.math.group';
                }
                update updateContato;
            }
            catch(Exception e){
                System.debug('Error' + e.getMessage());
            }
    }
}
```

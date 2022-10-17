# MÉTODOS GET, DELETE && POST

## CLASSE
```
@RestResource(urlMapping='/GetContactAPI/*')
global with sharing class getContactAPI {
    @HttpGet
    global static Contact doGet(){
        RestRequest req = RestContext.request;
        RestResponse res = RestContext.response;

        String contcId = req.requestURI.subString(req.requestURI.lastIndexOf('/')+1);
        Contact contcInfo = [SELECT Id, FirstName, LastName, Birthdate, Email, MailingAddress FROM Contact WHERE Id = :contcId];
        return contcInfo;
    }
    @HttpDelete
    global static void doDelete() 
    {
        RestRequest req = RestContext.request;
        RestResponse res = RestContext.response;
        String contcId = req.requestURI.substring(req.requestURI.lastIndexOf('/')+1);
        Contact result = [SELECT Id, FirstName, LastName, Email, MailingAddress, Birthdate FROM Contact WHERE Id = :contcId ];
        delete result;
        System.debug('Deletado');
    }

    @HttpPost
    global static String doPost(String FirstName, String LastName, String Email){
        Contact pcontc = new Contact();
        pcontc.FirstName = FirstName;
        pcontc.LastName = LastName;
        pcontc.Email = Email;
        insert pcontc;
        System.debug('Criado Contato no id: ' + pcontc.id);
        return pcontc.id;
    }
}
```
# WORKBENCH
> Link: https://workbench.developerforce.com/login.php
>> Marcar sandbox ou produção e logar
>>> Utilities -> Rest explorer

## GET NO WORKBENCH
- Formato do link será: */services/apexrest/NomeDaAPI(urlMapping)/ID*

Exemplo:
``` 
/services/apexrest/GetContactAPI/0030300000eTnHnAAK
```

## POST NO WORKBENCH
- Formato do link será: */services/apexrest/NomeDaAPI(urlMapping)*
- No request body preencher os campos com os parâmetros definidos no método (no mínimo os que forem obrigatórios)

Exemplo:
```
/services/apexrest/GetContactAPI

Request body

{
    "FirstName" : "Maíra",
    "LastName" : "Silva"
}

```

## DELETE NO WORKBENCH

```
/services/apexrest/GetContactAPI/0030300000eTnHnAAK
```



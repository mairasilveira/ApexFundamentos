## CLASSE
```
public with sharing class ContactTableController {  
    @AuraEnabled(cacheable=true)
    public static List<Contact> contactTableController() {
         return [SELECT Id,FirstName,LastName FROM Contact];
    }
}
```

## NO HTML DO LWC

```
<template>
    <div style ="height: 300px">
    <template if:true={contc}>
        <lightning-datatable key-field='id' columns={colunas} data={contc}></lightning-datatable>
    </template>
    <template if:true={error}>
        {error}
    </template>   
    </div>
</template>
```

## NO JAVASCRIPT DO LWC

```
import { LightningElement, track, wire } from 'lwc';
import contactTableController from '@salesforce/apex/ContactTableController.contactTableController';
export default class ContactTable extends LightningElement {
    @track colunas = [{
        FirstName: '',
        LastName:''
    },
    {
        label:'Primeiro Nome',
        fieldName:'FirstName',
        type:'text',
        sortable:true //setinha da coluna tabela para filtrar dados
    },
    {
        label:'Sobrenome',
        fieldName:'LastName',
        type:'text',
        sortable:true
    }]
     
    @track error;
    @track contc;
    @wire(contactTableController)
    wiredContacts({
        error,
        data
    }) {
        if (data) {
            this.contc = data;
        } else if (error) {
            this.error = error;0
        }
    }
```

## META.XML

```
<?xml version="1.0" encoding="UTF-8"?>
<LightningComponentBundle xmlns="http://soap.sforce.com/2006/04/metadata">
    <apiVersion>55.0</apiVersion>
    <isExposed>true</isExposed>
     <targets>
        <target>lightning__RecordPage</target>
        <target>lightning__HomePage</target>
        <target>lightning__AppPage</target>
    </targets>
</LightningComponentBundle>
```
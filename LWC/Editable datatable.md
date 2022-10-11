# NA CLASSE:
```
public with sharing class ContactTableController {  
    @AuraEnabled(cacheable=true)
    public static List<Contact> contactTableController() {
         return [SELECT Id, FirstName, LastName, OtherAddress, Email, Birthdate, Title FROM Contact];
    }
}
```
# HTML DO LWC:
```
<template>
    <div style ="height: 300px">
    <template if:true={contc}>
        <lightning-datatable key-field='Id' columns={colunas} data={contc} onsave={handleSave} draft-values={draftValues}></lightning-datatable>
    </template>
    <template if:true={error}>
        {error}
    </template>   
    </div>
</template>
```
# JAVASCRIPT DO LWC:
```
import { LightningElement, track, wire, api } from 'lwc';
import contactTableController from '@salesforce/apex/ContactTableController.contactTableController';
import { updateRecord } from 'lightning/uiRecordApi';
import { ShowToastEvent } from 'lightning/platformShowToastEvent';
import { refreshApex } from '@salesforce/apex';
import FIRSTNAME_FIELD from '@salesforce/schema/Contact.FirstName';
import LASTNAME_FIELD from '@salesforce/schema/Contact.LastName';
import TITLE_FIELD from '@salesforce/schema/Contact.Title';
import BIRTHDATE_FIELD from '@salesforce/schema/Contact.Birthdate';
import EMAIL_FIELD from '@salesforce/schema/Contact.Email';
import OTHER_ADDRESS_FIELD from '@salesforce/schema/Contact.OtherAddress'
export default class ContactTable extends LightningElement {

    // Cria as colunas da tabela
    @track colunas = [
    {
        label:'Primeiro Nome',
        fieldName:FIRSTNAME_FIELD.fieldApiName,
        type:'text',
        sortable:true,
        editable:true
    },
    {
        label:'Sobrenome',
        fieldName:LASTNAME_FIELD.fieldApiName,
        type:'text',
        sortable:true,
        editable:true
    },
    {
        label:'Data de Nascimento',
        fieldName:BIRTHDATE_FIELD.fieldApiName,
        type:'date',
        sortable:true,
        editable:true
    },
    {
        label:'Cargo',
        fieldName:TITLE_FIELD.fieldApiName,
        type:'text',
        sortable:true,
        editable:true
    },
    {
        label:'Endereço',
        fieldName:OTHER_ADDRESS_FIELD.fieldApiName,
        type:'text',
        sortable:true,
        editable:true
    },
    {
        label:'Email',
        fieldName:EMAIL_FIELD.fieldApiName,
        type:'email',
        sortable:true,
        editable:true
    }]
    
    // Adiciona conteúdo na tabela
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
            this.error = error;
        }
    }
    
    // Início do código para tornar o conteúdo da tabela editável
    draftValues = [];
    // columns = this.colunas;
    @track Contact;
    @wire(contactTableController)
    contactData(result) {
        this.Contact = result;
        console.log(result);
        if (result.error) {
            this.Contact = undefined;
        }
    };
    
    async handleSave(event) {
        // Convert datatable draft values into record objects
        const records = event.detail.draftValues.slice().map((draftValue) => {
            const fields = Object.assign({}, draftValue);
            return { fields };
        });

        // Clear all datatable draft values
        this.draftValues = [];

        try {
            // Update all records in parallel thanks to the UI API
            const recordUpdatePromises = records.map((record) =>
                updateRecord(record)
            );
            await Promise.all(recordUpdatePromises);

            // Report success with a toast
            this.dispatchEvent(
                new ShowToastEvent({
                    title: 'Success',
                    message: 'Contacts updated',
                    variant: 'success'
                })
            );

            // Display fresh data in the datatable
            await refreshApex(this.Contact);
        } catch (error) {
            this.dispatchEvent(
                new ShowToastEvent({
                    title: 'Error updating or reloading contacts',
                    message: 'Contacts failed',
                    variant: 'error'
                })
            );
        }
    }
}
```
# META-XML:
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
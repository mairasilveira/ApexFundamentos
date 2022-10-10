# CLASSE
```
public with sharing class TesteInsertController {
    @AuraEnabled
    public static void testeInsert(){

        List<Contact> contc = new List<Contact>();
        //Cria três contatos francisco targa
        for(Integer i=0;i<3;i++){
            contc.add(new Contact(FirstName='francisco',LastName='targa'));
      }
        insert contc;
    } 
}
```

# HTML
> Foram criados campos text, lookup, picklist, textarea para o componente. Ao clicar no botão é criado um contato

```
<template>
    <lightning-card title="Create Contact" icon-name="action:add_contact" class="slds-m-around_xx-large">

        <div class="slds-p-around_small">
            <lightning-button onclick={saveRecord} label="Create" value="Save Record" variant="success"></lightning-button>
        </div>

        <div class="slds-grid slds-wrap">
            <div class="slds-col slds-size_1-of-2 slds-p-around_small">
                <lightning-input type="text" name="FirstName" label="Nome" onchange={inputChange} value={ContactObject.FirstName} required></lightning-input>  
            </div>

            <div class="slds-col slds-size_1-of-2 slds-p-around_small">
                <lightning-input type="text" name="LastName" label="Sobrenome" onchange={inputChange} value={ContactObject.LastName} required></lightning-input>  
            </div>

            <div class="slds-col slds-size_1-of-2 slds-p-around_small">
                <lightning-input type="text" name="Title" label="Cargo" onchange={inputChange}></lightning-input>  
            </div>

            <div class="slds-col slds-size_1-of-2 slds-p-around_small">
                <c-picklist-component onselected={picklistChange} object-api-name="Contact" field-api-name="LeadSource" label="Lead Source"></c-picklist-component>
            </div>

            <div class="slds-col slds-size_1-of-2 slds-p-around_small">
                <lightning-input type="date" name="Birthdate" label="Data de Nascimento" date-style="long" onchange={inputChange}></lightning-input>
            </div>

            <div class="slds-col slds-size_1-of-2 slds-p-around_small">
                <c-custom-lookup onlookup={lookupChange} label="Reporta-se a" variant="label-stacked" object-api-name="Contact" iconname="standard:record" field-api-name="Name" relationshipfield="ReportsTold"></c-custom-lookup>
            </div>

            <div class="slds-col slds-size_1-of-2 slds-p-around_small">
                <lightning-textarea name="Address" label="Address"></lightning-textarea> 
            </div>
            
        </div>    
    </lightning-card>
</template>
```

# JAVASCRIPT
```
import { LightningElement, track, api, wire} from 'lwc';
import createContact from '@salesforce/apex/ContactController.createContact';
export default class ContactObject extends LightningElement {

    @track ContactObject = {
        Name: '',
        Title: '',
        LeadSource:'',
        Birthdate:'', 
        ReportsTold:'',
        Address:'',
        LastName:'',
    }

    inputChange(event){
        let apiName = event.target.name;
        let inputVal = event.target.value;
        this.ContactObject[apiName] = inputVal;
    }

    lookupChange(event){
        let selectedRecordId = event.detail.recordId;
        let lookupfield = event.detail.relationshipfield
        this.ContactObject[lookupfield] = selectedRecordId;
    }

    picklistChange(event){
        let PickVal = event.detail.picklistvalue;
        let fieldApiName = event.detail.fieldApiName;
        this.ContactObject[fieldApiName] = PickVal;
    }

    validateForm() {
        const allValid = [...this.template.querySelectorAll('lightning-input')].reduce((validSoFar, inputCmp) => {
            inputCmp.reportValidity();
            return validSoFar && inputCmp.checkValidity();
        }, true);
        let txtArea = [...this.template.querySelectorAll('lightning-textarea')];
        let allValidTxtArea;
        if (txtArea) {
            allValidTxtArea = txtArea.reduce((validSoFar, inputCmp) => {
                inputCmp.reportValidity();
                return validSoFar && inputCmp.checkValidity();
            }, true);
        }
        let isValid = allValid;
        if (txtArea) {
            isValid = allValid && allValidTxtArea;
        }
        return isValid;
    }
    
    saveRecord() {
        let allValid = this.validateForm();
        console.log('teste',JSON.stringify(this.ContactObject))
        if (allValid) {
            createContact({
                contactObj : JSON.stringify(this.ContactObject),
                accountId : this.ContactObject.accountId
            })
            .then(record => {
                window.console.log('record ', record);
            })
            .catch(error => {
                window.console.log('error', error)
            });
        }
    }
}
```

# META.XML
> Lembrar de ativar o isExposed para true
>> Acrescentou-se os targets: lightning__RecordPage, lightning__HomePage e lightning__AppPage
>>> Alterar masterLabel
```
<?xml version="1.0" encoding="UTF-8"?>
<LightningComponentBundle xmlns="http://soap.sforce.com/2006/04/metadata" fqn="AccountObject">
    <apiVersion>55.0</apiVersion>
    <isExposed>true</isExposed>
    <masterLabel>Contact Object</masterLabel>
    <targets>
        <target>lightning__RecordPage</target>
        <target>lightning__HomePage</target>
        <target>lightning__AppPage</target>
    </targets>
</LightningComponentBundle>
```
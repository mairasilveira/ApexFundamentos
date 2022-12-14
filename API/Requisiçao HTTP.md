# HTML
```
<template>
    <lightning-card
      variant="Narrow"
      title="Consulta de CEP"
      icon-name="action:map"
    >
      <template if:false={loaded}>
        <lightning-spinner alternative-text="Loading"></lightning-spinner>
      </template>
      <div class="slds-p-left_small slds-p-right_small">
        <lightning-input
          label="CEP"
          name="cep"
          value={cep}
          type="text"
          id="cep"
          max-length="9"
          onchange={handleChangeCEP}
          onblur={handleBlurCEP}
        ></lightning-input>
  
        <lightning-input
          label="Rua"
          name="rua"
          value={rua}
          type="text"
          id="rua"
        ></lightning-input>
  
        <lightning-input
          label="Bairro"
          name="bairro"
          value={bairro}
          type="text"
          id="bairro"
        ></lightning-input>
  
        <lightning-input
          label="Cidade"
          name="cidade"
          value={cidade}
          type="text"
          id="cidade"
        ></lightning-input>
  
        <lightning-input
          label="Estado"
          name="uf"
          value={uf}
          type="text"
          id="uf"
        ></lightning-input>
      </div>
      <div slot="footer">
        <lightning-button label="Salvar"></lightning-button>
      </div>
    </lightning-card>
  </template>
```

# JAVASCRIPT
```
import { LightningElement, track } from 'lwc';

const urlViacep = 'https://viacep.com.br/ws/';

export default class ConsultaCEP extends LightningElement {

    @track cep;
    @track rua;
    @track bairro;
    @track cidade;
    @track uf;
    @track loaded = true;

    handleChangeCEP(event) {
        this.cep = event.target.value;
    }

    handleBlurCEP(event) {
        this.loaded = false;
        fetch(`${urlViacep + this.cep}/json/`, // End point URL
            {
                // Request type
                method: "GET",
            })
            .then((response) => {
                return response.json(); // returning the response in the form of JSON
            })
            .then((jsonResponse) => {

                let responseObj = jsonResponse;

                this.cep = responseObj['cep'];
                this.rua = responseObj['logradouro'];
                this.bairro = responseObj['bairro'];
                this.cidade = responseObj['localidade'];
                this.uf = responseObj['uf'];

                this.loaded = true;
            })
            .catch(error => {
                window.console.log('callout error ===> ' + JSON.stringify(error));
            })
    }
}
```
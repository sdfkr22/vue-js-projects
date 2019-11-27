<template>
<div class="container shadow-lg p-3 mb-5 bg-white rounded">
  <h1>Converter</h1>
  <hr>
  <br>
  <p class="mb-0 text-info">Please enter a binary number</p>
  <input 
  @input="$v.binNum.$touch()" 
  :class="{'is-invalid' : !$v.binNum.regex}" 
  class="form-control" 
  v-model="binNum"
  @keypress="onKeyPressForBinary" 
  >
  <br>
  <p class="mb-0 text-info">Please enter a decimal number</p>
  <input 
  class="form-control" 
  :value="convertToDec()"  
  @input="convertDecToBin($event.target.value)"
  @keypress="onKeyPressForDecimal"
  >
  <br>
  <p class="mb-0 text-info">Please enter a hexadecimal number</p>
  <input 
  class="form-control" 
  :value="convertToHex()" 
  @input="convertHexToBin($event.target.value)"
  @keypress="onKeyPressForHexaDecimal"
  >
 
</div>
  
</template>

<script>

import {required, numeric, between, helpers} from "vuelidate/lib/validators"
const regex = helpers.regex(this.binNum, /[0-1]*/)
export default {
  data() {
    return {
      binNum : null,
      decNum : null,
      hexNum : null,
    }
    
  },
  
  validations : {
    binNum : {
      numeric,
      regex,
    }
  },
  methods : {
    convertToDec(){
      if(this.binNum){
        return this.decNum = parseInt(this.binNum, 2).toString(10);
      }
      this.decNum = null;
       
    },
    convertToHex(){
      if(this.binNum){
        return this.hexNum = parseInt(this.binNum, 2).toString(16).toUpperCase();
      }
      this.hexNum = null;
      
    },
    convertDecToBin(decNum){
      if(decNum){
        return this.binNum = parseInt(decNum, 10).toString(2);
      }
      this.binNum=null;
       
    },
    convertHexToBin(hexNum){
      if(hexNum){
        return this.binNum = parseInt(hexNum, 16).toString(2);
      }
      this.binNum=null;
      
    },

    onKeyPressForBinary(event){
      const char = String.fromCharCode(event.keyCode)
    	if (!/[0-1]/.test(char)) {
      	event.preventDefault();
      }
    },

    onKeyPressForDecimal(event){
      const char = String.fromCharCode(event.keyCode)
    	if (!/[0-9]/.test(char)) {
      	event.preventDefault();
      }
    },

    onKeyPressForHexaDecimal(event){
      const char = String.fromCharCode(event.keyCode)
      console.log("inside")
    	if (!/[0-9A-Fa-f]/.test(char)) {
      	event.preventDefault();
      }
    },
  },
}

</script>

<style>

</style>

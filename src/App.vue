<template>
  <div id="app">
<!--    <img alt="Vue logo" src="./assets/logo.png">-->
    <div class="container">
      <!--Header Section-->
      <header id="title">
        <h1>Number Converter</h1>
      </header>

      <!--   Main content section -->
      <main>
        <!--    Main system converstion -->
        <section id="number-system">
          <h2>Number System Converstion</h2>
          <div class="box">
            <div class="input-group">
              <label>Decimal </label>
              <input type="text" placeholder="decimal" v-model="number.decimal">
            </div>
            <div class="input-group">
              <label>Binary </label>
              <input type="text" placeholder="Binary" v-model="number.binary">
            </div>
            <div class="input-group">
              <label>Hexa </label>
              <input type="text" placeholder="Hexa" v-model="number.hexa">
            </div>
            <div class="input-group">
              <label>Octal </label>
              <input type="text" placeholder="octal" v-model="number.octal">
            </div>

            <div class="reset-btn-container">
              <p v-if="invalidNumber" style="color: red"> Invalid Input </p>
              <button v-on:click="resetNumber">Reset</button>
            </div>
            <div class="one-rem-space"></div>
          </div>
        </section>
        <!--    Text converstion -->
        <section id="text-system">
          <h2>Text Converstion</h2>
          <div class="box">
            <div class="input-group">
              <label>Enter your text below</label>
              <textarea name="text-field" cols="40" rows="10"> </textarea>
            </div>
            <div class="half-rem-space"></div>

            <div class="input-group">
              <label>Enter your Binary  below</label>
              <textarea name="binary-field" cols="40" rows="10"> </textarea>
            </div>
            <div class="reset-btn-container">
              <button>Button</button>
            </div>
            <div class="one-rem-space"></div>
          </div>
        </section>


      </main>
    </div>


  </div>
</template>

<script>
 // import HelloWorld from './components/HelloWorld.vue'

require('@/assets/css/reset.css')
require('@/assets/css/fonts.css')
require('@/assets/css/style.css')

function isBinary(text){
  for(let b of text){
    if(b!=='1' &&  b!=='0')
       return false
  }
  return true
}

function isOctal(text){
  for(let octal of text){
    if(octal< '0' || octal > '8') return false
  }
  return true
}


function  ishexa(text){
  for(let hex of text){
    if((hex<'0' || hex >'9') && (hex<'a' || hex >'f') && (hex<'A' || hex >'F')) return false;
  }
  return true;
}

export default {

  name: 'App',
  // components: {
  //    HelloWorld
  // }
  data(){
    return  {
      number:{
        decimal: 0,
        binary:0,
        hexa:0,
        octal:0
      },
      invalidNumber:false
    }
  },
  methods:{
    resetNumber(){
      this.number={
        decimal: 0,
        binary:0,
        hexa:0,
        octal:0
      },
     this.invalidNumber=false
    }
  },

  watch:{
    'number.decimal':function (value){
      this.number.decimal=parseInt(value) || 0;
      this.number.binary=value.toString(2);
      this.number.octal=value.toString(8);
      this.number.hexa=value.toString(16);
    },
    'number.binary':function (value){
      let decimal=parseInt(value,2);

      if (!isBinary(value)) {
          this.invalidNumber=true
      }
      else{
        this.invalidNumber=false
      }
      this.number.decimal=decimal;
      this.number.binary=value || 0;
      this.number.octal=decimal.toString(8);
      this.number.hexa=decimal.toString(16);
    },
    'number.octal':function (value){
      let decimal=parseInt(`0${value}`,8) || 0;
       if (!isOctal(value)){
         this.invalidNumber=true
       }
       else {
         this.invalidNumber=false
       }
       this.number.decimal=decimal;
       this.number.binary=decimal.toString(2) || 0;
       this.number.octal=value || 0;
       this.number.hexa=decimal.toString(16)
    },
    'number.hexa':function (value){
      let decimal=parseInt(`0x${value}`,16) || 0
      if(!ishexa(value)){
        this.invalidNumber=true
      }
      else {
        this.invalidNumber=false;
      }
      this.number.decimal=decimal;
      this.number.binary=decimal.toString(2) || 0;
      this.number.octal=decimal.toString(8);
      this.number.hexa=value || 0
    }
  }
}
</script>

<style>

</style>

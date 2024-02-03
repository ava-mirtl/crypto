<script >
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
export default {
components: {
  Input, Selector
},
data(){
  return {
amount: 0,
error: '',
cryptoFirst: '',
cryptoSecond: '',  }
},
methods:{
  changeAmount(val){
    this.amount = val
  },
  setCryptoFirst(val){
    this.cryptoFirst = val
  },
  setCryptoSecond(val){
    this.cryptoSecond = val
  },
  convert(){
    if(this.amount <=0){
      this.error="Введите число больше ноля";
      return;
    }
    else if(this.cryptoFirst == ''|| this.cryptoSecond == ''){
      this.error="Выберите валюту";
      return;
    }
    else if(this.cryptoFirst == this.cryptoSecond){
      this.error="Выберите другую валюту";
      return;
    }
   
    this.error = '';
  }
}
}
</script>

<template>
<h1>CRYPTO</h1>
<Input :changeAmount="changeAmount" :convert="convert"/>
<p v-if="error!=''" class="error">{{ error }}</p>
<div className="selectors">
<Selector :setCrypto="setCryptoFirst"/>
<Selector :setCrypto="setCryptoSecond"/>
</div>

</template>

<style scoped>
h1{
  font-family: 'Nabla', system-ui;
  font-size: 10em;
}
.selectors{
  display: flex;
  justify-content: space-around;
  width: 650px;
  margin: 0 auto;
}
.error{
  color: brown;
  margin-bottom: 20px;
}
</style>

<script >
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import CryptoConvert from 'crypto-convert';

const convert = new CryptoConvert();

export default {
components: {
  Input, Selector
},
data(){
  return {
amount: 0,
error: '',
cryptoFirst: '',
cryptoSecond: '', 
result: 0 }
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
  async convert() {
  if (this.amount <= 0) {
    this.error = "Введите число больше ноля";
    return;
  } else if (this.cryptoFirst == "" || this.cryptoSecond == "") {
    this.error = "Выберите валюту";
    return;
  } else if (this.cryptoFirst == this.cryptoSecond) {
    this.error = "Выберите другую валюту";
    return;
  }

  this.error = "";
  await convert.ready();

  switch (this.cryptoFirst + "-" + this.cryptoSecond) {
    case "BTC-ETH":
      this.result = convert.BTC.ETH(this.amount);
      break;
    case "BTC-USDT":
      this.result = convert.BTC.USDT(this.amount);
      break;
    case "ETH-BTC":
      this.result = convert.ETH.BTC(this.amount);
      break;
    case "ETH-USDT":
      this.result = convert.ETH.USDT(this.amount);
      break;
    case "USDT-BTC":
      this.result = convert.USDT.BTC(this.amount);
      break;
    case "USDT-ETH":
      this.result = convert.USDT.ETH(this.amount);
      break;
    default:
      this.result = 0; // или установите какое-то допустимое значение по умолчанию
      break;
  }
}
}
}
</script>

<template>
<h1>CRYPTO</h1>
<Input :changeAmount="changeAmount" :convert="convert"/>
<p v-if="error!=''" class="error">{{ error }}</p>
<p v-if="result!=0" class="result_text">{{ result }}</p>

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
.result_text{
  font-family: 'Nabla', system-ui;
  font-size: 2em;
  margin-bottom: 20px;
;
}
</style>

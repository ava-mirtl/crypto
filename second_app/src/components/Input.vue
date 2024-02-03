<script>
export default{
props:{
  changeAmount:{
    type: Function,
    required: true
  },
  convert:{
    type: Function,
    required: true
  }
}
}
</script>

<template>
<input min='0' type="number" @input="changeAmount($event.target.value)" placeholder="Введите число">
<br/>
<button @click="convert()">Конвертировать</button>
</template>

<style scoped>
input{
  outline: none;
  border-radius: 3px;
  width: 500px;
  font-size: 1.2em;
  border: 0;
  padding: 10px 15px;
  background: #fafafa;
  color: #333;
  margin-bottom: 20px;
}
button{
  padding: 15px 20px;
  color: #fff;
  text-transform: uppercase;
  cursor: pointer;
  background: #1a032d;
  border: 0;
  border-radius: 3px;
  margin-bottom: 20px;
}
</style>

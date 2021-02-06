<template>
  <div style="display: inline-block;">
    <div id="firstCol">
                Number : <b-form-input type="number" v-model="num" placeholder="Enter your name" @input="onChangeSelect"></b-form-input>
    </div>
    <div id="secondCol">
    <b-form-select v-model="selected" :options="options" @change="onChangeSelect"></b-form-select>
    </div>
    <div id="thirdCol">
    {{textDisplay}}
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      num: 1,
      selected: null,
        options: [
          { value: null, text: 'Please select a method'},
          { value: 'prime', text: 'isPrime' },
          { value: 'fibo', text: 'isFibonacci' },
        ],
      textDisplay: 'Please select something first',
    }
  },
  methods:{
    toInt(){
      this.num = Math.round(this.num);
      if(Number.isNaN(this.num)||this.num===undefined||this.num==null||this.num<1){
      	this.num=1
      }
      console.log(this.num)
    },
    checkSQR(num){
        var a = parseInt(Math.sqrt( num ));
        return (num * num == a);
    },
    isFibo(num, count = 1, last = 0){
      if(count < num){
          return this.isFibo(num, count+last, count);
      };
      if(count === num){
          return true;
      }
      return false;
    },
    isPrime(n){
        if (n===1)
        {
            return false;
        } else if(n === 2)
        {
            return true;
        } else
        {
            for(var x = 2; x < n; x++)
            {
            if(n % x === 0)
            {
                return false;
            }
            }
            return true;  
        }
    },
    onChangeSelect(){
      this.toInt()
      if(this.selected==null){
        this.textDisplay = 'Please select something first'
      } else if(this.selected=='prime'){
        this.textDisplay = this.isPrime(this.num)
      } else if(this.selected=='fibo'){
        this.textDisplay = this.isFibo(this.num)
      } else {
        this.textDisplay = `Please don't mess around`
      }
    }
  }
}
</script>

<style>
#firstCol{
    width: 200px;
    height: 30vh;
    display: inline-block;
    top: 0px;
}
#secondCol{
    min-width: 100px;
    width: auto;
    height: 30vh;
    display: inline-block;
    overflow-x: scroll;
    top: 0px;
}
#thirdCol{
    width: 300px;
    height: 30vh;
    display: inline-block;
    top: 0px;
}
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>

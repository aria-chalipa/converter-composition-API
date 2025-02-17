<template>
  <div class="div">
    <valueCom :value="valueOutput.valueInput.value" @inputt="handleInputValue" />
    <fromCom :value="valueOutput.valueFrom" @inputt="handleInputFrom" />
    <toCom :value="valueOutput.valueTo" @inputt="handelInputTo"/>

    <outputCom :value="valueOutput"/>

  </div>
</template>

<script>
import { reactive, watch} from "vue";
import valueCom from './converter/valueCom.vue';
import fromCom from './converter/fromCom.vue';
import toCom from './converter/toCom.vue'
import outputCom from './converter/outputCom.vue'

export default {
  name: 'converCom',
  components: {
    valueCom,
    fromCom,
    toCom,
    outputCom
  },
  setup() {

    const valueOutput = reactive({ 
        valueInput: {
          value: null,
        },
        valueFrom: null,
        valueTo: null
      });
      
      watch(()=> valueOutput
      , (newValue)=>{
        console.log(newValue)
      })


    // watchEffect(() => {
    //   valueOutput.value = {
    //     valueInput: valueInput.value,
    //     valueFrom: valueFrom.value,
    //     valueTo: valueTo.value
    //   };
    // });

    
    function handleInputValue(value) {

      const isNumber = isNaN(value.data)
      if (isNumber) {
        alert('please inter a number')
        
      }
      
      valueOutput.valueInput.value = value.data; 
    }

    function handleInputFrom(value) {
     valueOutput.valueFrom = value.data;
    } 
    
    function handelInputTo(value) {
      valueOutput.valueTo= value.data
    }







    return { valueOutput, handleInputValue, handleInputFrom, handelInputTo };
  },
};
</script>


<style scoped>
  .div {
    font-family: Arial, sans-serif;
    margin: 20px;
    width: 70%;
    display: flex;
    justify-content: center;
    /* align-items: center; */
    flex-direction: column;
    margin: auto;
    border: solid 2px #F0F0F0;
    border-radius: 10px;
    padding: 20px;
    box-shadow: 5px 5px 100px black;
  }

  h2 {
    color: #333;
    font-size: 24px;
  }

  .error {
    color: red;
    font-weight: bold;
  }

  input {
    padding: 10px;
    margin: 5px 0;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%;
    display: inline;
    margin: 10px;
  }
  lable{
    display: inline;
  }

</style>
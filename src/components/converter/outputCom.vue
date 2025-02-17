<template>
  <div>
    <div>
      <h2>{{ out }}, {{ Input.valueTo }}</h2>
      <div v-if="errorV" style="color: red;">Error: From and To currencies cannot be the same!</div>
    </div>
  </div>
</template>

<script>
import { ref, watchEffect } from 'vue';


export default{
    props:['value'],
  
    setup(p){
      let Input = ref({
      valueFrom: '',
      valueTo: '',
      valueInput: ''
    });
    let out = ref('');
    let errorV = ref(false);
       

        watchEffect(() => {
          Input.value = p.value;
          errorV
          validationOut()
          calculation()
       });


         function validationOut() {
          errorV.value = Input.value.valueFrom === Input.value.valueTo;
        }
    
        
        function calculation(){

          const from = Input.value.valueFrom
          const to = Input.value.valueTo
          const value = parseFloat(Input.value.valueInput.value)

          if (from === 'dolar' && to === 'real') {
        out.value = value * 90000;
      } else if (from === 'dolar' && to === 'euro') {
        out.value = value * 1.04;
      } else if (from === 'dolar' && to === 'tr') {
        out.value = value * 11.62;
      } else if (from === 'real' && to === 'dolar') {
        out.value = value / 90000;
      } else if (from === 'real' && to === 'euro') {
        out.value = value / 93100;
      } else if (from === 'real' && to === 'tr') {
        out.value = value / 248000;
      } else if (from === 'euro' && to === 'dolar') {
        out.value = value / 1.04; // Corrected conversion rate
      } else if (from === 'euro' && to === 'real') {
        out.value = value * 93100;
      } else if (from === 'euro' && to === 'tr') {
        out.value = value * 37.18;
      } else if (from === 'tr' && to === 'dolar') {
        out.value = value / 11.62; // Corrected conversion rate
      } else if (from === 'tr' && to === 'real') {
        out.value = value * 24800;
      } else if (from === 'tr' && to === 'euro') {
        out.value = value / 37.18;
      } else {
        out.value = 'Invalid conversion';
      }
        }


        return{Input,validationOut,calculation,out,errorV}

    }
}

</script>

<style>


</style>
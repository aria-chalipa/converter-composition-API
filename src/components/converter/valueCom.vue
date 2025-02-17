<template>
  <div>
    <label for="value">value</label>
    <input v-model="localValue" @input="emitValue" />
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  props: {
    value: {
      type: String,
    }
  },
  setup(props, { emit }) {
     
    const localValue = ref(props.value);

    const emitValue = () => {

      emit('inputt', { data: localValue.value });
    };

    return { localValue, emitValue };
  },
};
</script>

<style scoped>
  div {
    margin: 10px 0;
  }

  label {
    font-weight: bold;
    margin-right: 10px;
  }

  input {
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%;
    font-size: 16px;
  }

  input:focus {
    border-color: #007BFF;
    outline: none;
  }
</style>

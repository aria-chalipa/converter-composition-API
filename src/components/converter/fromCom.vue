<template>
  <div>
    <label for="from">from</label>
    <select v-model="localSelected" @change="emitValue">
      <option v-for="(option, index) in options" :key="index" :value="option">
        {{ option }}
      </option>
    </select>
  </div>
</template>

<script>
import { ref, watch } from "vue";

export default {
  props: {
    value: {
      type: String,
    }
  },
  setup(props, { emit }) {
    const options = ['dolar', 'real', 'euro', 'tr'];
    const localSelected = ref(props.value);

    watch(() => props.value, (newValue) => {
      localSelected.value = newValue;
    });

    const emitValue = () => {
      emit('inputt', { data: localSelected.value });
    };

    return { localSelected, options, emitValue };
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

  select {
    padding: 8px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%;
    font-size: 16px;
  }

  select:focus {
    border-color: #007BFF;
    outline: none;
  }
</style>

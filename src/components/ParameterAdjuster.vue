<!-- ParameterAdjuster.vue -->
<template>
    <div>
      <input type="number" v-model="newParameter" placeholder="New Parameter Value">
      <button @click="adjustParameters">Adjust Parameters</button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ParameterAdjuster',
    data() {
      return {
        newParameter: 0
      };
    },
    methods: {
      adjustParameters() {
        this.$emit('adjust-parameters', this.newParameter);
        this.newParameter = 0;
      }
    }
  }
  </script>
  
  <style>
  /* Add your styles here */
  </style>
  
<!-- Screen2.vue -->
<template>
    <div>
      <fairness-checker @check-fairness="checkFairness"></fairness-checker>
      <parameter-adjuster @adjust-parameters="adjustParameters"></parameter-adjuster>
    </div>
  </template>
  
  <script>
  import FairnessChecker from '@/components/FairnessChecker.vue';
  import ParameterAdjuster from '@/components/ParameterAdjuster.vue';
  
  export default {
    name: 'Screen2',
    components: {
      FairnessChecker,
      ParameterAdjuster
    },
    methods: {
      checkFairness() {
        
      },
      adjustParameters(params) {
        
      }
    }
  }
  </script>
  
  <style>
  /* Add your styles here */
  </style>
  
<!-- BiasChecker.vue -->
<template>
    <div class="bias-checker">
      <button @click="checkBias" class="check-bias-btn">Check Bias</button>
      <p v-if="biasDetected" class="bias-info">Bias Detected!</p>
      <p v-else class="bias-info">No Bias Detected</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'BiasChecker',
    data() {
      return {
        biasDetected: false
      };
    },
    methods: {
      checkBias() {
        // Implement bias checking logic here
        // Set this.biasDetected accordingly
      }
    }
  }
  </script>
  
  <style scoped>
  .bias-checker {
    text-align: center;
  }
  
  .check-bias-btn {
    background-color: #e50914;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .check-bias-btn:hover {
    background-color: #d30813;
  }
  
  .bias-info {
    margin-top: 10px;
    font-size: 16px;
    color: #fff;
  }
  </style>
  
  
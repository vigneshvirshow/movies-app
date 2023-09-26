<template>
    <div class="search-box">
      <input
        type="text"
        v-model="query"
        placeholder="Find a movie..."
        @input="handleInput"
      />
      <button class="search-button" @click="search">Search</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        query: ''
      };
    },
    methods: {
      handleInput() {
        this.$emit('search', this.query);
      },
      search() {
        // Call a search function or API endpoint when the button is clicked
        this.$emit('search', this.query);
      }
    }
  };
  </script>
  
  <style scoped>
  .search-box {
    margin: 10px;
  }
  .search-box input {
    padding: 5px;
    width: 200px;
    margin-right: 5px;
  }
  .search-button {
    padding: 6px 12px;
    background-color: #4CAF50;
    color: white;
    border: none;
    cursor: pointer;
  }
  .search-button:hover {
    background-color: #45a049;
  }
  </style>
  
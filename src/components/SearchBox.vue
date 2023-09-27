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
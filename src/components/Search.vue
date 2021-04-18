<template>
  <div id="search-container">
    <input type="text"
      v-model="query"
      v-on:input="$emit('query-change', query)">
  </div>
</template>

<script lang="ts">

interface Query {
  query: string
}

export default {
  name: 'Search',
  data() :Query {
    return {
      query: '',
    };
  },
};
</script>

<style lang="scss">
  #search-container{
    width: 600px;
    margin: 0 auto;
  }

  input{
    padding: 10px;
    width: 100%;
    outline: none;
  }
</style>

<template>
  <div class="container">
    <div class="card my-3 shadow text-danger">
      <div class="card-header">
        <h2 class="text-center">Biography</h2>
      </div>
      <div class="card-body">
        <div v-for="item in Object.keys(passed_data)" class="d-flex justify-content-between px-4 py-2">
          <p>{{ item }}</p>
          <p class="biography-item">{{ passed_data[item] }}</p>
        </div>
        <h3 class="text-center my-3 p-2">Aliases (Alternate names)</h3>
        <ul>
          <li v-for="item in aliase">{{ item }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'biography',
    data() {
      return {
        aliase: this.passed_data.aliases
      }
    },
    props: {
      passed_data: {
        required: true,
        type: Object
      }
    },
    methods: {

    },
    created() {

    }
  }
</script>

<style lang="scss" scoped>
  .card-body {
    ul {
      background-color: coral;
      color: #FFF;
      font-family: 'Gupter', serif;
      list-style-type: none;
      font-size: 1.2rem;
      padding: 0.5rem;

      li {
        margin: 1rem auto;
      }
    }
  }
</style>

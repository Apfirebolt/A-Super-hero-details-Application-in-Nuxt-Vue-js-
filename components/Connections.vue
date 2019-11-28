<template>
  <div class="container">

    <div class="card my-3 shadow text-danger">
      <div class="card-header">
        <h2 class="text-center">Connections Container</h2>
      </div>
      <div class="card-body">
        <p class="custom_header">
          Groups
        </p>
        {{ passed_data }}
        <p class="custom_header">
          Relatives
        </p>

        {{ passed_data.relatives }}
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'connections',
    data() {
      return {
        relatives: [],
        teams: []
      }
    },
    props: {
      passed_data: {
        required: true,
        type: Object
      }
    },
  }
</script>

<style lang="scss" scoped>
  .custom_header {
    text-align: center;
    background-color: transparent;
    border: 1px solid green;
    padding: 0.5rem;
    margin-top: 1rem;
    margin-bottom: 1rem;
  }
</style>

<template>
  <div class="container">
    <div class="card my-3 shadow text-danger">
      <div class="card-header"><h2 class="text-center">Power Stats</h2></div>
      <div v-for="item in Object.keys(passed_data)" class="d-flex justify-content-between px-4 py-2">
        {{ item|capitalize }} <p class="stats-item">{{ passed_data[item] }}</p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'power_stats',
    props: {
      passed_data: {
        required: true,
        type: Object
      }
    },
    filters: {
      capitalize(value) {
        return value.charAt(0).toUpperCase() + value.slice(1)
      }
    }
  }
</script>

<style lang="scss" scoped>
  .stats-item {
    border-radius: 50%;
    background-color: #47494e;
    padding: 1rem;
    color: white;

  }
.d-flex {
  p {
    font-size: 1.2rem;
  }
}
</style>

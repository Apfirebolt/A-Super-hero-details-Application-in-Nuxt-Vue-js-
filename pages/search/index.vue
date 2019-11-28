<template>
  <div class="container">
    <div>
      <h2 class="title">
        All your favorite Marvel and DC Heroes under same API!
      </h2>

      <div class="image_container">
        <div class="inner-image">
          <img src="~assets/images/dc_logo.jpg" alt="Image not available" />
        </div>
        <div class="inner-image">
          <img src="~assets/images/marvel-logo.jpg" alt="Image not available" />
        </div>
      </div>

      <div class="container d-flex justify-content-between my-4">
        <div class="form-group w-100 text-center">
          <label for="character_name">Enter the Name of the character</label>
          <input type="text" class="form-control" name="character_name" id="character_name" v-model="character_name">
        </div>
      </div>

      <div class="container">
        <button class="btn w-100 detail_button" @click="getData">Get Character details</button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        isLoading: false,
        character_name: '',
        character_id: 0
      }
    },
    methods: {
      getData: function() {
        this.$router.push(`/search/${this.character_name}`);
      }
    },
    components: {

    }
  }
</script>

<style lang="scss" scoped>
  .title {
    font-family: 'Titillium Web', sans-serif;
    display: block;
    font-weight: 500;
    font-size: 2.5rem;
    color: azure;
    letter-spacing: 1px;
    padding: 1rem;
    text-align: center;
  }

  .image_container {
    display: flex;
    justify-content: space-between;


    img {
      width:100%;
      height:100%;
    }
    .inner-image {
      width: 40%;
      box-shadow: 2px 2px 3px #fff;
    }
  }

  .detail_button {
    width: 50%;
    margin: auto;
    background-color: crimson;
    color: #FFF;
    font-family: Verdana, sans-serif;
    font-size: 1.5rem;
  }
</style>

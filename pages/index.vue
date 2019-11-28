<template>
  <div class="container-fluid">
    <div>
      <div class="landing">
        <p>Welcome to the Super Hero API page where you can see the details of basically every super hero there is
        </p>

        <nuxt-link to="/search" class="custom_link">List All Superheroes/Villains</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'

export default {
  data() {
    return {
      change_class: 'none-display'
    }
  },
  components: {
  },
  methods: {

  },
  mounted() {

  }
}
</script>

<style lang="scss" scoped>

.container-fluid {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.landing {
  width: 80%;
  position: absolute;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  top: 300px;
  background-color: darkslategray;
  border-radius: 2rem;
  animation: display_animation 2s forwards;

}

@keyframes display_animation {
  0% {
    display: none;
    background-color: darkslategray;
  }

  100% {
    display: block;
    background-color: orangered;
  }
}



</style>

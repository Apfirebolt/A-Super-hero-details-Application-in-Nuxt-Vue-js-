<template>
  <div class="container-fluid">
    <div>
      <nav>
        <div class="nav-item" :class="selected_tab == 'power' ? 'active' : null"
             @click="selected_tab = 'power'">Power Stats</div>
        <div class="nav-item" :class="selected_tab == 'bio' ? 'active' : null"
             @click="selected_tab = 'bio'">Biography</div>
        <div class="nav-item" :class="selected_tab == 'connection' ? 'active' : null"
             @click="selected_tab = 'connection'">Connections</div>
        <div class="nav-item" :class="selected_tab == 'appearance' ? 'active' : null"
             @click="selected_tab = 'appearance'">Appearance</div>
        <div :class="selected_tab == 'work' ? 'active' : null"
             class="nav-item" @click="selected_tab = 'work'" >Work</div>
      </nav>

      <div class="container text-center my-3">
        <button class="btn-large btn-danger px-3" @click="$router.go(-1)">Go Back</button>
      </div>

      <div v-if="total_results.length == 0" class="container text-center">
        <pulse-loader :loading="loading" :color="color" :size="size">
        </pulse-loader>
        <h2 v-if="error_text" class="text-danger bg-dark p-2 my-3 rounded">{{ error_text }}</h2>
      </div>

      <div class="container" v-else>
        <div v-if="total_results.length > 1" class="container-fluid">
          <h2 class="text-center text-white my-3">
            Multiple results were retrieved for your query. Currently, <span class="text-primary bg-white p-2">{{ current_name }}</span>
            is selected. You can toggle selected super-hero by clicking buttons given below.
          </h2>
          <div class="container-fluid d-flex justify-content-between">
            <button v-for="(hero, index) in total_results" class="w-100 hero_button"
                    @click="setData(index)" :key="index">
              {{ hero.name }}
            </button>
          </div>
        </div>

        <h2 class="text-danger bg-white shadow p-2 my-4 text-center" v-else>{{ current_name }}</h2>

        <img :src="current_image.url" alt="Image not available" height="300" width="300" class="rounded mx-auto d-block">

        <div class="container-fluid">
          <appearance-component v-if="selected_tab == 'appearance'" :passed_data="appearance"></appearance-component>
          <biography-component v-else-if="selected_tab == 'bio'" :passed_data="biography"></biography-component>
          <power-stats v-else-if="selected_tab == 'power'" :passed_data="power"></power-stats>
          <connections-component v-else-if="selected_tab == 'connection'" :passed_data="connection"></connections-component>
          <work-component v-else :passed_data="work"></work-component>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import Logo from '~/components/Logo.vue'
  import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
  import axios from 'axios'
  import AppearanceComponent from '~/components/Appearance.vue'
  import WorkComponent from '~/components/Work.vue'
  import BiographyComponent from '~/components/Biography.vue'
  import PowerStats from '~/components/PowerStats.vue'
  import ConnectionsComponent from '~/components/Connections.vue'

  export default {
    data() {
      return {
        current_hero: this.$route.params.name,
        color: 'red',
        size: '100px',
        loading: false,
        current_name: '',
        current_image: {},
        work: {},
        appearance: {},
        biography: {},
        power: {},
        connection: {},
        total_results: [],
        selected_tab: 'appearance',
        error_text: ''
      }
    },
    components: {
      PulseLoader,
      AppearanceComponent,
      WorkComponent,
      BiographyComponent,
      PowerStats,
      ConnectionsComponent
    },
    methods: {
      setData(current_index) {
        this.current_name = this.total_results[current_index].name;
        this.work = this.total_results[current_index].work;
        this.power = this.total_results[current_index].powerstats;
        this.connection = this.total_results[current_index].connections;
        this.appearance = this.total_results[current_index].appearance;
        this.biography = this.total_results[current_index].biography;
        this.current_image = this.total_results[current_index].image;
      },
      loadApiData: function() {
        this.loading = true;
        axios
          .get(
            `https://cors-anywhere.herokuapp.com/https://superheroapi.com/api/${process.env.API_KEY}/search/${this.current_hero}`
          )
          .then(res => {
            if(res.data.error) {
              this.error_text = res.data.error;
              return;
            }
            let current_data = res.data.results;
            this.total_results = current_data;
            this.current_name = current_data[0].name;
            this.work = current_data[0].work;
            this.power = current_data[0].powerstats;
            this.connection = current_data[0].connections;
            this.appearance = current_data[0].appearance;
            this.biography = current_data[0].biography;
            this.current_image = current_data[0].image;
            this.loading = false;
          })
          .catch(err => console.log(err));
      }
    },
    mounted() {
      this.loadApiData();
    }
  }
</script>

<style lang="scss" scoped>
  nav {
    margin-top: 1rem;
    margin-bottom: 2rem;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    text-align: center;

    div.nav-item {
      border: 2px solid mintcream;
      background: greenyellow;
      padding: 0.8rem;
      min-width: 140px;
      font-family: 'Gupter', serif;
      transition: all 1s ease-out;
      text-align: center;
      border-radius: 0.5rem;
      font-size: 1.5rem;
      color: #47494e;
      margin: 1rem;
    }

    div.nav-item:hover {
      background-color: mintcream;
      color: #47494e;
      border-radius: 2rem;
      transition: all 1s ease-out;
      cursor: pointer;
    }
  }

  .hero_button {
    box-shadow: 2px 2px 2px #FFF;
    background-color: #F5F5F5;
    border: none;
    box-radius: 1rem;
    padding: .3rem;
    margin: 1rem;
    transition: all 0.5s ease-out;
    font-family: 'Titillium Web', sans-serif;
    font-size: 1.5rem;
  }

  .hero_button:hover {
    color: #fff;
    background-color: transparent;
    border: 3px solid indianred;
    transition: all 0.5s ease-out;
    box-shadow: none;
  }

  .active {
    background-color: crimson !important;
    color: white !important;
  }
</style>

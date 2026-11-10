<template>
  <div id="app">
    <img id="logo" alt="Vue logo" src="./assets/logo.png">
    <SearchVehicleForm @show-selected-vehicle="setSelectedVehicle"/>
    
    <div class="selected-vehicle" v-if="selectedVehicle">
      <strong>Selected vehicle: </strong>{{ selectedVehicle }}
    </div>
  </div>
</template>

<script>
import SearchVehicleForm from './components/SearchVehicleForm.vue'

export default {
  name: 'App',
  components: {
    SearchVehicleForm
  },
  
  data() {
    return  {
      selectedVehicle: null,
    };
  },

  methods: {
    setSelectedVehicle(vehicleData) {
        this.selectedVehicle = vehicleData.join(' ');
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;

  #logo {
    width: 100%;
    max-width: 250px;
    margin: 10px 0 30px;
  }

  .selected-vehicle {
    font-size: 20px;
    margin: 20px 10px;
  }
}
</style>

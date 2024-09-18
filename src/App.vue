<template>
  <div>
    <header>
      <img src="./assets/pokemon.png" />
    </header>
    <div class="pokebola">
      <img src="./assets/pokebola.png" />
    </div>

    <main>
      <div class="pokemon" v-for="pokemon in pokemones" :key="pokemon.id">
        <img :src="pokemon.imagen" alt="" />
        <h2>{{ pokemon.nombre }}</h2>
        <div class="power">
          <p>{{ pokemon.type_name }}</p>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      pokemones: [],
    };
  },
  create() {
    this.getPokemon();
  },
  methods: {
    async getPokemon() {
      try {
        const response = await axios.get(
          "https://cobuses.com.co/APIV2/model/pokemon.php?dato=getallpokemon"
        );
        this.pokemones = response.data;
        console.log(response.data);
      } catch (error) {
        console.error("El error es: " + error);
      }
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

header {
  width: 100%;
  height: 100px;
  background: #000;
  display: flex;
  justify-content: center;
  align-items: center;
}

header img {
  height: 90%;
}

.pokebola {
  width: 100%;
  height: 60px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.pokebola img {
  height: 90%;
}
</style>

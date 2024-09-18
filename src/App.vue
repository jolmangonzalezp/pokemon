<template>
  <div id="app">
    <header>
      <img src="./assets/pokemon.png" alt="Pokémon Logo" />
    </header>
    <div class="pokebola">
      <img src="./assets/pokebola.png" alt="Pokeball" />
    </div>

    <main>
      <div class="pokemon" v-for="pokemon in pokemones" :key="pokemon.id">
        <img :src="pokemon.imagen" :alt="pokemon.nombre" />
        <h2>{{ pokemon.nombre }}</h2>
        <div class="power" :style="{ background: pokemon.type_color }">
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
  created() {
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

main {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  padding: 20px;
}

.pokemon {
  margin: 10px;
  padding: 10px;
  border-radius: 8px;
  width: 150px;
  text-align: center;
}

.pokemon img {
  max-width: 100%;
  height: auto;
}
</style>

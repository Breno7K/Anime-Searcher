<template>
  <div id="app">
    <header>
      <h1>Anime Searcher</h1>
    </header>
    <form class="search_form" @submit.prevent="getAnimes">
      <input
        type="search"
        class="search-field"
        placeholder="E.g. naruto"
        required
        v-model="input"
      />
      <button class="s_btn" type="submit">Go</button>
    </form>
    <section class="animes" v-if="animelist.length > 0">
      <AnimeCard
        v-for="anime in animelist"
        :key="anime.mal_id"
        :anime="anime"
      />
    </section>

    <section class="animes" v-else>
      <h2>Nothing found yet...</h2>
    </section>

    <footer>
      Made with &#128153; by
      <a href="https://github.com/Breno7K" target="_blank">Breno</a>
    </footer>
  </div>
</template>

<script>
import { ref } from "vue";
import AnimeCard from "./components/AnimeCard.vue";

export default {
  components: { AnimeCard },

  setup() {
    const animelist = ref([]);
    const input = ref();

    const getAnimes = async () => {
      animelist.value = await fetch(
        `https://api.jikan.moe/v4/anime?q=${input.value}`
      )
        .then((response) => response.json())
        .then((animesJson) => animesJson.data);

      console.log(animelist.value);
    };

    return {
      getAnimes,
      input,
      animelist,
    };
  },
};
</script>



<style lang="scss" >
* {
  padding: 0%;
  margin: 0%;
  box-sizing: border-box;

font-family: 'Roboto', sans-serif; 
letter-spacing: 2px;
  text-decoration: none;
  font-weight: bold;
}

body {
  background: #FFCACA;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

#app {
  min-height: 100%;
  color: #372948;
}

header {
  margin: 50px 0px;
  h1 {
    
    text-align: center;
    font-size: 4.7rem;
    font-weight: bolder;
  }
}

.search_form {
  display: flex;
  justify-content: center;
  margin: 0% 2%;

  input {
    width: 100%;
    max-width: 520px;
    padding: 10px;
    margin: 0px 0px 50px 0px;
    font-size: 20px;
  }

  button{

    background-color: #FFECEF;
    max-height: 48px;
    padding: 0px 8px;

    border: 1px solid ;
    border-radius: 0px;

    margin-right: 1%;

    &:hover{
      cursor: pointer;
      background: #372948;
      color: #FFECEF;
      

    }
  }
  
}

.animes {
  border-radius: 15px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  column-gap: 3%;
  width: 75vw;
  margin: 0% auto;
  background: #251B37;
  color: #FFECEF;

  padding: 5%;
}

footer {
  margin: 15px 0px;
  text-align: center;

  a{
    color: #251B37;
    &:hover{
      text-decoration: underline;
    }
  }
}
</style>

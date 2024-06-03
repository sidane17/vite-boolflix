<script >
import AppHeader from './components/AppHeader.vue'
import store from '../data/store.js';
export default {
  components: {
    AppHeader,
  },data(){
    return{
      store,
      search:"",
      image:"https://image.tmdb.org/t/p/w342/"
    }
  },
  methods:{
    getFilms(){
      
    }
  },
  mounted(){
     axios.get("https://api.themoviedb.org/3/search/movie?api_key=c27807fa81b43a83930bd41ed474cb4a&query=ritorno+al+futuro").then(risultato=>{
      this.store.films=risultato.data.results;
      console.log(this.store.films)
      
      
    }),
    axios.get("https://api.themoviedb.org/3/search/tv?api_key=c27807fa81b43a83930bd41ed474cb4a&language=it_IT&query=scrubs").then(r=>{
      this.store.serie=r.data.results;
      console.log(r.data.results)
    })
  
  }
}
  
</script>

<template>
  <div class="container">
  <div class="head d-flex flex-column">
    <label for="search">Cerca</label>
    <input type="text" placeholder="cerca titolo" v-model="search">
    <button  @click="getFilms">Invia</button>
  </div>
  <div class="containerCard" >
    <div class="card" v-for="film in this.store.films">
      <img :src="this.image + film.backdrop_path" alt="" width="" height="60%">
      <p>{{ film.title }}</p>
      <p>{{ film.original_title}}</p>
      <p>{{ film.original_language }}</p>
      <p>{{ film.vote_average }}</p>
    </div>
    <div class="card" v-for="serie in this.store.serie">
      <img :src="this.image + serie.poster_path" alt="" width="" height="60%">
      <p>{{ serie.name }}</p>
      <p>{{ serie.original_name}}</p>
      <p>{{ serie.original_language }}</p>
      <p>{{ serie.vote_average }}</p>
    </div>
  </div>
</div>
</template>

<style scoped>
.head{
  width: 15rem;
  height: fit-content;
}
.containerCard{
  display: flex;
  flex-wrap: wrap;
  height: fit-content;
  width: 100%;
  border-style: dashed;
  overflow: scroll;

}
.card{
  border-style: dashed;
  width:15rem;
  height: 25rem; 
   background-color: rgb(34, 34, 34);
   color: white;
}
image{
  height: 50%;
  height: 100%;
}
p{
  font-size: 0.8rem;
}
</style>

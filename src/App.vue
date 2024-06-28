<template>
  <div class="app">
    <header>
      <h1>The <strong>Movie</strong> Database</h1>
      <form class="search-box" v-on:submit='handleSearch'>
        <input
         type="search"
         class="searchField" 
         placeholder="search for a movie..."
         v-model = "search_query">
      </form>
    </header>
 </div>
 <main>
  <div class="cards">
    <card v-for="movie in movieList" :aa="movie"/>
    <!-- aa라는 이름으로 movie 가 전달됨 -->
     </div>
 </main>
</template>

<script setup>

  import card from './components/Card.vue'
  import { ref } from 'vue'
  
  const movieList = ref([]);
  const search_query = ref('');

  const popular = async() => {
    movieList.value = await fetch('https://api.themoviedb.org/3/movie/popular?language=en-US&page=1&api_key=e1d7e960d2ba6a1023905edcc927293d')
     .then(response => response.json())
     .then(data => data.results)
  }
  
  popular()

  const handleSearch = async() => {
    movieList.value = await fetch(`https://api.themoviedb.org/3/search/movie?query=${search_query.value}&include_adult=false&language=en-US&page=1&api_key=e1d7e960d2ba6a1023905edcc927293d`)
     .then(response => response.json())
     .then(data => data.results)
    
     search_query.value = ""
    }
  
    handleSearch()
</script>


<style lang="scss" scoped>
 $color : #313131;
 * { 
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif
 }
 header {
  padding: 50px;
  h1 {
    color: #999;
    text-align: center;
    font-weight: 400px;
    box-sizing: border-box;
    strong {
      color: $color;
    }
  }
 }
 .search-box {
  display: flex;
  justify-content: center;
  padding: 0 30px;
  .search-field{
    appearance: none;
    border: none;
    outline: none;
    padding: 15px;
    width: 100%;
    max-width: 600px;
    border-radius: 8px;

    font-size: 20px;
    color: $color;
    background-color: aliceblue;
    box-shadow: 0 4px 8px rgba(0,0,0,0.3);

    &::placeholder{
     color: #aaa;
    }
    
  
  }
 }
 main {
      max-width: 1200px;
      margin:auto;
      padding: 0 16px;
    
      .cards {
        display: flex;
        flex-wrap: wrap;
        border: 2px solid blue;
        

      }
    }
</style>

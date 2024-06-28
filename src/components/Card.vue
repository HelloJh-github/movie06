<template>
  <div class="card">
    <a v-vind:href="'https://www.themoviedb.org/movie/'+aa.id">
      <figure>
        <img v-if="aa.poster.path" 
        :src="'https://image.tmdb.org/t/p/w600_and_h900_bestv2'+aa.poster_path" 
        :alt="aa.title">
        <img v-else  
        src="http://placehold.it/200x300/aaa/333?text=MoviePoster" 
        :alt="aa.title">
      </figure>
      <div class="text">
        <h3>{{ aa.title }}</h3>
        
      </div>
    </a>
  </div>
</template>

<script setup>
 const props = defineProps(['aa'])




</script>


<style lang="scss">
 $tablet: '(max-width: 860px)';
 $mobile: '(max-width: 600px)';

  .card {
    padding: 16px;
    width: 25%;

    @media ($tablet) {
      width: 33.33%;
    }
    @media ($mobile) {
      width: 50%;
    }
    
    a {
      display: block;
      text-decoration: none;
      border-radius: 16px;
      overflow: hidden;
      box-shadow: 0 4px 8px rgba(0,0,0,0.3);
    
      figure {
        width: 100%;
        height: 360px;
        overflow: hidden;
        margin: 0px;
        img{
          width: 90%; height: 90%; object-fit: cover;
          margin-top: 20px;
          object-fit: cover;
          transition: 0.3s;
        }
      }
      .text {
       /*  border: 2px solid red; */
        height: 80px;
        padding: 16px;

        

        
      }
      h3 {
          color: #313131;
          font-size: 16px;
        }
    }
   &:hover a h3 {
    color: rgb(145, 201, 201);
    transform: scale(0.8);
   }
   &:hover img {
    transform: scale(1.5);
   }
  }

</style>

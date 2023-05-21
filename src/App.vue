<script setup>
import GamesList from './components/GamesList.vue';
import GenresBox from './components/GenresBox.vue';
import SearchBar from './components/SearchBar.vue';


</script>

<template>

      <div class="game-box">
        <SearchBar/>  
        <GamesList/>
      </div>
      <GenresBox/>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400&display=swap');
html, body {
  height:100%;
  font-family: 'Roboto', sans-serif;
  min-height: 100vh;
}
body{
  background: linear-gradient(rgba(209,209,209,1) , rgba(97,104,106,1) );
  background-repeat: no-repeat;
  background-attachment: fixed;
}
.game-box{
display:flex;
margin: 5px;
flex-direction: column;


}





header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>

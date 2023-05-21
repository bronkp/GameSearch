<script>
import { BiStarFill } from "oh-vue-icons/icons";

import { OhVueIcon, addIcons } from "oh-vue-icons";
addIcons(BiStarFill);
export default {
  props: {
    game: Object
  }
  , components: {
    "v-icon": OhVueIcon
  }
}
</script>

<template>
  <div class="game-container">
    <div class="rating"><v-icon scale="1.3" color="white" name="bi-star-fill" /><p>{{ game?.rating }}</p></div>
    <div class="title" ><a :href="'https://www.google.com/search?q='+game?.title">{{ game?.title }}</a></div>
    <div class="team"><p>{{ game?.release }}</p></div>


    <div  class="genres">
      <div class="genre" v-for="genre in game?.genres">
        <p> {{ genre }}</p>
      </div>
    </div>
  </div>
</template>
<style scoped>
.genre {
  justify-content: center;
  align-items: center;
  display: flex;
  height:3vh;
  padding-right: 3px;
  padding-left: 3px;
  border-radius: 5px;
  margin-right: 2px;
  min-width: 60px;
  background-color: rgb(94, 94, 94);
}

.genre>p {
  color: #FFFBFE;
}
p{
 color: #FFFBFE
}
a{
  text-decoration: none;
  font-size: 2vw;
  font-weight: 500;
  color:#FFFBFE;
}
.game-container {
  display: grid;
  padding: 10px;
  border-radius: 15px;
  box-sizing: border-box;
  grid-template-areas:
    'rating rating title title '
    'team team team team'
    'genres genres genres genres';
 row-gap: 0px;
  margin: 11px;
 
  background-color: #818182;
}


.rating{
  grid-area: rating;
  padding-right: 20px;
  align-items: center;
  display: flex;
}
.rating>p {
  font-size: 2vw;
  padding-left: 2px;
  color: white;
}
.team {
  grid-area: team;
}

.title {
  display:flex;
  justify-content: flex-end;
  font-size: large;
  font-family: Roboto;
  grid-area: title;
}

.genres {
  display: flex;
  flex-direction: row;
  grid-area: genres;
}
</style>
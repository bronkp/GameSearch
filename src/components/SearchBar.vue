<script>
import { getDocs, query, where, } from '@firebase/firestore';
import { gamesRef } from '../firebase';
import { store } from '../store.js'
export default {
  data() {
    return {
      store,
      
      
    }
  },
  methods: {
    async getSearch(search) {
      try {
        

        //Capitalizing first letter of seach and only searches from first 3 letter
        //very basic way but gets probably every game
        const split = search.split('')
        split[0] = split[0]?.toUpperCase()
        search = split.splice(0, 4).join('')
        const q = query(gamesRef, where('title', '>=', search), where('title', '<=', search + '\uf8ff'))
        const results = await getDocs(q)
        const newList = []
        results.forEach(game => newList.push(game.data()))
        //removes all duplicate entries, many in the data set
        const uniqueTitles = []
        const uniqueGames = []
        newList.map(game => {
          if (!uniqueTitles.includes(game.title)) {
            uniqueTitles.push(game.title); uniqueGames.push(game) 
          }
        }
        )
        store.games = uniqueGames
      } catch (error) {
        console.log('getSearch error',error)
      }
    

      }
  }
}
</script>
<template>
  <div class="search-container">
    <input class="search-bar" @change="store.search = $event.target.value" type="text" />
    <button class="search-button" @click="getSearch(store.search)">Search</button>
  </div>
</template>

<style scoped>
.search-bar{
  border-radius: 10px 0px 0px 10px;
  max-width: 65vw;
  min-width:500px;
  border-width: 0px;

  font-size: 3vh;
}
.search-button{
  cursor:pointer;
  border-width: 0px;
  background-color: rgb(234, 232, 232);
  border-radius: 0px 10px 10px 0px;
  
}
.search-container{
  display: flex;
  flex-direction: row;
  margin:30px;
  height:5vh;
  max-width: 80vw;
  top: 5px;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
}
</style>
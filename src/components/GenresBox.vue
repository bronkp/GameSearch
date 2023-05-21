<script>
import { useCollection } from 'vuefire'
import { collection, query, where, limit, getDocs, orderBy } from 'firebase/firestore'
import { gamesRef } from '../firebase'
import { store } from '../store'


export default {
    data() {
        return {
            genres: ['RPG', 'Adventure', 'Platform','Turn Based Strategy','Simulator','Real Time Strategy','Indie','Fighting', 'Shooter','MOBA'],
            checkedGenres: []
        }
    },

    methods: {
        async setChecked(genre, checked) {
            try {
                //checks if genre already checked, if it is it removes it from array
                if (checked) {
                    this.checkedGenres.push(genre)
                } else {
                    var index = this.checkedGenres.indexOf(genre);
                    if (index >= 0) {
                        this.checkedGenres.splice(index, 1);
                    }
                }

                const q = query(gamesRef, where('genres', 'array-contains-any', this.checkedGenres), orderBy('rating','desc'), limit(30));
                const results = await getDocs(q);
                const newList = []
      results.forEach(game => newList.push(game.data()))
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
                console.log(error)
            }

        },
    }
}
</script>
<template>
    <div class="check-container">
        <p>Genres</p>
        <div class="genre" v-for="genre in genres">
            <p>{{ genre }}</p> 
            <input class="check" type="checkbox" @change="setChecked(genre, $event.target.checked)" />
        </div>
    </div>
</template>
<style scoped>
.check{
    position: absolute;
    top:0px;
    bottom:0px;
    margin: auto;
    right:5px;
    padding-left: 5px;
}
p {
    margin-right: 6px;
    color: #FFFBFE;
}

input {
    margin: 4px;
}

.genre {
    background-color: #848585;
    position: relative;
    display: flex;
    flex-direction: row;
    padding-right: 3px;
    margin-right:5px;
    margin-left: 5px;
}

.check-container {
    position: absolute;
    width:10vw;
    gap:4px;
    min-width: 150px;
   
    border-radius: 10px;
    right: 10px;
    top: 100px;
    padding: 3px;
    background-color: #7A7D7D;
    display: flex;
    flex-direction: column;
}
</style>
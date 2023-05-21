
<script>
import { store } from '../store'
import Game from './Game.vue';
export default {
    data() {
        return {
            store
        };
    },
    components: { Game }
}

</script>
<template>
    <div class="list">
        <!-- 
        v-for function can be used like a .map in jsx
        then a Game component is generated on each loop
        : before game signifies props to be passed.
     -->
        <div v-if="store.games.length">

            <Game v-for="game in store.games" :game="game" />
        </div>
        
            <h1 v-else>Pick some genres or search for specific title</h1>

    </div>
</template>
<style scoped>
h1{padding-left: 10px; color: #656565;}
p {
    color: black;
}

.no-games {
    background-color: rgba(220, 223, 220, 0.539);
    height: 600px;
    width: 600px;
}

.list {
    width: 60vw;
    max-width: 1000px;
    border-radius: 10px;
    left: 5vw;
    top: 5vh;
    display: flex;
    flex-direction: column;
    background-color: #bbbbbb;
}</style>
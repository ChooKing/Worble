<script setup lang="ts">  
  import Board from './components/Board.vue';  
  import  { useGameStore, Letter } from "./stores/game";
  import { onMounted } from "vue";
  const game = useGameStore();
  game.setAnswer();
  const guesses = game.$state.guesses;
  onMounted(
  ()=>{
    document.onkeydown = processKey;
  });
  function processKey(event: KeyboardEvent){
    if ((event.key.length ==1)&&(game.col<game.wordLength)&&/[a-zA-Z]/.test(event.key)){
      game.processLetter(event.key.toUpperCase() as Letter);
    }            
    else if((event.key=="Backspace")&&(game.row<game.maxGuesses)){    
        game.processBackspace();
    }  
    else if((event.key=="Enter")&&(game.col==game.wordLength)){
        game.processEnter();
    }          
}
</script>


<template>
  <h1>Worble</h1>
  <Board/>
  <span>By <a href="https://github.com/ChooKing/Worble" target="blank">Choo King</a> based on Wordle&trade;</span>
</template>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    
  }
  body{
    background-color: #0d2236;
  }
  h1{
    color: white;
    font-size: 4em;
    margin: 0.25em 0;
  }
  @media only screen and (max-width: 600px){
    h1{font-size: 10vw;}
  }
</style>

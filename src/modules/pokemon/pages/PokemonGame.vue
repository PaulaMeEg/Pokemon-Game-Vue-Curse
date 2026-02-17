<template>
   <section v-if="isLoading || !randomPokemon || randomPokemon.id === null" class="flex flex-col justify-center items-center w-screen h-screen">
    <h1 class ="text-3xl">Espere por favor</h1>
    <h3 class="animate-pulse">Cargando Pokémons</h3>
   </section>

   <section v-else class="flex flex-col justify-center items-center w-screen h-screen">
    <h1 class="m-5"> ¿Quien es este Pokemon?</h1>
    <div class="h-20">
    <button v-if="gameStatus!==GameStatus.Playing" 
    class="bg-gray-400 text-white p-2 rounded-md hover:bg-gray-600 transition-all"
    @click="getNextRound(4)">
    Jugar de nuevo
   </button>
   </div>

    <!-- Pokemon picture -->
     <PokemonPicture :pokemon-id="randomPokemon.id" 
     :show-pokemon="gameStatus !== GameStatus.Playing" />

    <!-- Pokeom options -->
     <PokemonOptions 
     :options="options"
     :block-selection="gameStatus !== GameStatus.Playing"
     :correct-answer="randomPokemon.id"
      @selected-option="checkAnswer"/>
   </section>
</template>

<script setup lang="ts">
import PokemonOptions from '../components/PokemonOptions.vue';
import PokemonPicture from '../components/PokemonPicture.vue';
import { usePokemonGame } from '../composables/usePokemonGame';
import { GameStatus } from '../interfaces';

const {
   randomPokemon, 
   isLoading, 
   gameStatus, 
   pokemonOptions: options, 
   checkAnswer, 
   getNextRound} = usePokemonGame();


</script>


<template>
  <TicTacToe :items="Arr">
    
  </TicTacToe>
</template>

<script>
import TicTacToe from '@/components/TicTacToe.vue'
export default {
  data(){
    return{
      Arr:[["j","j","j"],["j","j","j"],["j","j","j"]]
    }
  },
  components:{
    TicTacToe,
  }
}
</script>

<style>

</style>

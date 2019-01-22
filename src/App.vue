<template>
  <div id="app">
    <GameVersionTable></GameVersionTable>
  </div>
</template>


<script>
import GameVersionTable from './components/GameVersionTable';

export default {
  name: 'app',
  components: {
    GameVersionTable
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

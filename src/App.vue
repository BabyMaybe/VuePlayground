<template>
  <div id="app">

    <BasicHeader adj="cute"></BasicHeader>
    <SimpleList v-for="i in items" :num=i v-bind:key=i />
  </div>
</template>


<script>
import BasicHeader from './components/BasicHeader';
import SimpleList from './components/SimpleList';

export default {
    name: 'app',
    components: {
        BasicHeader,
        SimpleList
    },
    data: function() {
        return {
            items: ['apples', 'bananas', 'cranberries', 'dates', 'elderberries', 'figs']
        };
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

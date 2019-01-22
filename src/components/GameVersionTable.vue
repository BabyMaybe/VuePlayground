<template>
  <table>
    <thead>
      <tr>
        <td class="header" @click="sortGen">Generation</td>
        <td class="header" @click="sortRegion">Region</td>
        <td class="header" @click="testFunc">Games</td>
        <td class="header" @click="sortSpecies">New Species</td>
        <td class="header" @click="sortTypes">New Types</td>
      </tr>
    </thead>
    <tbody>
      <GameItem v-for="g in sortedGames" :key="g.name" :game="g"/>
    </tbody>
  </table>
</template>

<script>
import GameItem from './GameItem';

export default {
  name: 'GameVersionTable',
  components: {
    GameItem
  },
  data: function() {
    return {
      games: []
    };
  },
  created: function() {
    this.loadData();
  },
  computed: {
    sortedGames: function() {
      return this.games;
    }
  },
  methods: {
    loadData: async function() {
      console.log('loading data');
      const rootURL = 'https://pokeapi.co/api/v2/generation/';
      let response = await fetch(rootURL);
      let data = await response.json();
      const gameEndpoints = data.results;

      let gameEndpointPromises = gameEndpoints.map(g => {
        return fetch(g.url).then(response => response.json());
      });

      this.games = await Promise.all(gameEndpointPromises);
      console.log(this.games);
    },
    testFunc: function() {
      console.log('this is a test');
      this.games.reverse();
    },
    sortGen: function() {
      console.log('sorting gen');
      this.games.sort((a, b) => a.name > b.name);
    },
    sortRegion: function() {
      console.log('sorting region');
      this.games.sort((a, b) => {
        if (a.game.main_region.name > b.game.main_region.name) {
          return 1;
        }
        if (a.game.main_region.name < b.game.main_region.name) {
          return -1;
        }
        return 0;
      });
    },
    sortSpecies: function() {
      console.log('sorting species');
    },
    sortTypes: function() {
      console.log('sorting type');
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Staatliches');
table {
  width: 100%;
  border-spacing: 0;
}

.header {
  background: black;
  color: white;
  padding: 1em;
  font-family: 'Staatliches', cursive;
  letter-spacing: 2px;
}

tr {
  background: lightgrey;
}

tr:nth-child(even) {
  background: white;
}

ul {
  list-style: none;
  text-align: left;
}
</style>

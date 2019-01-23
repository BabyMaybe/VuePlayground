<template>
  <table>
    <thead>
      <tr>
        <td class="header" @click="sortGen">Generation</td>
        <td class="header" @click="sortRegion">Region</td>
        <td class="header">Games</td>
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
            games: [],
            sortBy: 'generation',
            ascending: true,
            sortFn: (a, b) => a.typeslength - b.types.length
        };
    },
    created: function() {
        this.loadData();
    },
    computed: {
        sortedGames: function() {
            this.ascending = !this.ascending;

            return this.games.sort(this.sortFn);
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
        },
        testFunc: function() {
            console.log('this is a test');
            this.games.reverse();
        },
        sortGen: function() {
            console.log('sorting gen');
            this.sortFn = (a, b) => {
                let result = 0;
                if (a.name > b.name) {
                    result = 1;
                }
                if (a.name < b.name) {
                    result = -1;
                }
                return this.ascendingCheck(result);
            };
        },
        sortRegion: function() {
            console.log('sorting region');
            this.sortFn = (a, b) => {
                let result = 0;
                if (a.main_region.name > b.main_region.name) {
                    result = 1;
                }
                if (a.main_region.name < b.main_region.name) {
                    result = -1;
                }
                return this.ascendingCheck(result);
            };
        },
        ascendingCheck: function(result) {
            return this.ascending ? result * -1 : result;
        },
        sortSpecies: function() {
            this.sortFn = (a, b) => {
                let result = 0;
                if (a.pokemon_species.length > b.pokemon_species.length) {
                    result = 1;
                }
                if (a.pokemon_species.length < b.pokemon_species.length) {
                    result = -1;
                }
                return this.ascendingCheck(result);
            };
        },
        sortTypes: function() {
            this.sortFn = (a, b) => {
                let result = 0;
                if (a.types.length > b.types.length) {
                    result = 1;
                }
                if (a.types.length < b.types.length) {
                    result = -1;
                }
                return this.ascendingCheck(result);
            };
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
    cursor: pointer;
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

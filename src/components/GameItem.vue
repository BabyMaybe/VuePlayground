<template>
  <tr>
    <td>{{game.name}}</td>
    <td>{{game.main_region.name}}</td>
    <td>
      <ul>
        <li v-for="g in gameList" :key="g">{{g}}</li>
      </ul>
    </td>
    <td>{{game.pokemon_species.length}}</td>
    <td>{{game.types.length}}</td>
  </tr>
</template>


<script>
export default {
  name: 'GameItem',
  data: function() {
    return {
      gen: 'gen',
      region: 'region',
      games: 'games',
      species: 'species',
      types: 'types',
      gameList: []
    };
  },
  props: {
    url: String,
    game: Object
  },
  created: function() {
    this.gameList = this.game.version_groups.map(g => g.name);
  }
  //   methods: {
  //     loadData: function() {
  //       fetch(this.url)
  //         .then(res => res.json())
  //         .then(data => {
  //           console.log(data);
  //           this.gen = data.name;
  //           this.region = data.main_region.name;
  //           this.games = data.version_groups.map(g => g.name);
  //           this.species = data.pokemon_species.length;
  //           this.types = data.types.length;
  //         });
  //     }
  //   },
  //   computed: {
  //     gameList: function() {
  //       console.log(this.game.version_groups.map(g => g.name));
  //       return this.game.version_groups.map(g => g.name);
  //     }
  //   }
};
</script>

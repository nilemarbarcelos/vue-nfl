<template>
  <div class="hello">
    <div id="games" v-for="(game, key) in games">
      {{ game.network }} | {{ game.home.name }} {{ game.home.score }} - {{ game.away.score }} {{ game.away.name }}
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',
  data: () => ({
    games: [],
  }),
  created() {
    axios.get('https://scores-nfl.herokuapp.com/nfl-scores/2017/11')
      .then(response => {
        this.games = response.data.games
      })
  }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

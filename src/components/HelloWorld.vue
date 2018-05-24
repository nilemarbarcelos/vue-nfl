<template>
  <div class="hello">
    <button v-on:click="prevWeek()">Prev</button>
    <button v-on:click="nextWeek()">Next</button>
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
    week: 0
  }),
  created() {
    this.nextWeek()
  },
  methods: {
    prevWeek() {
      if (this.week > 1)
        this.week -= 1
      this.fetchWeek()
    },
    nextWeek() {
      if (this.week < 17)
        this.week += 1
      this.fetchWeek()
    },
    fetchWeek() {
      axios.get('https://scores-nfl.herokuapp.com/nfl-scores/2017/' + this.week)
      .then(response => {
        this.games = response.data.games
      })
    }
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

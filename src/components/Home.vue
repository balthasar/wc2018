<template>
  <div class="home">
    <img src="../assets/logo.png">
    <template v-if="live">
      <h3>Live</h3>
      <Match :match="currentMatch"></Match>
    </template>
    <div>
      <h3>Today's Matches</h3>
      <p v-show="today === false">There aren't any matches today</p>
      <template v-for="(match, index) in todaysMatches">
        <Match :match="match" :key="index"/>
      </template>
    </div>
  </div>

</template>

<script>
import Match from './Match.vue';

export default {
  name: 'Home',
  data: function() {
    return {
      currentMatch: {},
      todaysMatches: [],
      live: null,
      today: null
    };
  },
  components: {
    Match
  },
  created: function() {
    this.fetchLive();
    this.fetchToday();
  },

  methods: {
    fetchLive: function() {
      this.$http
        .get('http://worldcup.sfg.io/matches/current')
        .then(response => {
          console.log(response);
          if (response.body && response.body.length > 0) {
            this.currentMatch = response.body[0];
            this.live = true;
          }
        });
    },

    fetchToday: function() {
      this.$http.get('http://worldcup.sfg.io/matches/today').then(response => {
        console.log(response);
        if (response.body && response.body.length > 0) {
          this.todaysMatches = response.body;
          this.today = true;
        } else {
          this.today = false;
        }
      });
    }
  }
};
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
img {
  width: 60%;
}
</style>

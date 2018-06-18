<template>
  <div class="home">
    <loading :active.sync="fetching" :can-cancel="false"></loading>

    <img src="../assets/logo.png">
    <template v-if="live">
      <h3>Live</h3>
      <QuickMatch :match="currentMatch"></QuickMatch>
    </template>
    <div>
      <h3>Today's Matches</h3>
      <p v-show="today === false">There aren't any matches today</p>
      <template v-for="(match, index) in todaysMatches">
        <QuickMatch :match="match" :key="index"/>
      </template>
    </div>
  </div>

</template>

<script>
import QuickMatch from './QuickMatch.vue';
import ENUMS from '../common/constants.js';
import Loading from 'vue-loading-overlay';
import 'vue-loading-overlay/dist/vue-loading.min.css';

export default {
  name: 'Home',
  data: function() {
    return {
      currentMatch: {},
      todaysMatches: [],
      live: null,
      today: null,
      fetching: false
    };
  },
  components: {
    QuickMatch,
    Loading
  },
  created: function() {
    this.fetching = true;
    this.fetchLive();
    this.fetchToday();
  },

  methods: {
    fetchLive: function() {
      this.$http.get(ENUMS.URL + '/matches/current').then(response => {
        if (response.body && response.body.length > 0) {
          this.currentMatch = response.body[0];
          this.live = true;
        }
        this.fetching = false;
      });
    },

    fetchToday: function() {
      this.$http.get(ENUMS.URL + '/matches/today').then(response => {
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

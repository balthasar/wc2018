<template>
  <div class="all">
    <h3>All Matches</h3>
    <template v-for="(match, index) in matches">
      <Match :match="match" :key="index"/>
    </template>
    <p v-show="fetched === false">There is an error getting all the matches</p>
  </div>
</template>

<script>
import Match from './Match.vue';

export default {
  name: 'AllMatches',
  data: function() {
    return {
      matches: {},
      fetched: null
    };
  },
  components: {
    Match
  },
  created: function() {
    this.fetch();
  },
  methods: {
    fetch: function() {
      this.$http
        .get('http://worldcup.sfg.io/matches/?by_date=ASC')
        .then(response => {
          if (response.body && response.body.length > 0) {
            this.matches = response.body;
            this.fetched = true;
          } else {
            this.fetched = false;
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

<template>
  <div class="all">
    <loading :active.sync="fetching" :can-cancel="false"></loading>
    <h3>All Matches</h3>

    <template v-for="(match, index) in matches">
      <QuickMatch :match="match" :key="index"/>
    </template>
    <p v-show="error">There is an error getting all the matches</p>
  </div>
</template>

<script>
import QuickMatch from './QuickMatch.vue';
import ENUMS from '../common/constants';
import Loading from 'vue-loading-overlay';
import 'vue-loading-overlay/dist/vue-loading.min.css';

export default {
  name: 'AllMatches',
  data: function() {
    return {
      matches: {},
      fetching: false,
      error: false
    };
  },
  components: {
    QuickMatch,
    Loading
  },
  created: function() {
    this.fetch();
  },
  methods: {
    fetch: function() {
      this.fetching = true;
      this.$http.get(ENUMS.URL + '/matches/?by_date=ASC').then(
        response => {
          if (response.body && response.body.length > 0) {
            this.matches = response.body;
          } else {
            this.error = false;
          }
          this.fetching = false;
        },
        reponse => {
          this.error = true;
          this.fetching = false;
        }
      );
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

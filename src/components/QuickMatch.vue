<template>
  <div class="match">
    <div class="info">
      <div class="team home-team">
        {{match.home_team.country}}
        <img class="team-img" v-bind:src="teamSrc(match.home_team.code)" />
      </div>
      <div class="divider">
       {{match.home_team.goals}} - {{match.away_team.goals}}
       </div>
      <div class="team away-team">
        <img class="team-img" v-bind:src="teamSrc(match.away_team.code)" />
         {{match.away_team.country}}
      </div>
    </div>
    <div class="clear" />
  </div>
</template>

<script>
export default {
  name: 'QuickMatch',
  props: {
    match: {}
  },
  methods: {
    teamSrc: function(code) {
      return require('../assets/teams/' + code.toLowerCase() + '.png');
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
.match {
  border: 1px solid lightgrey;
  margin: 10px auto;
  max-width: 500px;
  vertical-align: middle;
}

.clear {
  clear: both;
  display: block;
}

.team {
  display: inline-block;
  width: 45%;
}

.divider {
  display: inline-block;
  width: 10%;
}

.home-team {
  text-align: right;
}

.away-team {
  text-align: left;
}

.team-img {
  height: 40px;
  vertical-align: middle;
}
</style>

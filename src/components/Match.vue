<template>
  <div class="match">
    <h4> {{match.home_team.country}} vs {{match.away_team.country}}</h4>
  </div>
</template>

<script>
export default {
  name: 'Match',
  props: {
    match: {}
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
</style>

<template>
  <div id="app">
      <p>
        <!-- use router-link component for navigation. -->
        <!-- specify the link by passing the `to` prop. -->
        <!-- `<router-link>` will be rendered as an `<a>` tag by default -->
        <router-link to="/">Home</router-link>
        <router-link to="/all">All Matches</router-link>
      </p>
      <router-view />
    <!-- //<Home /> -->
  </div>
</template>

<script>
export default {
  name: 'app',
  components: {}
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

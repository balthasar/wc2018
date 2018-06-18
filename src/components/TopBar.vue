<template>
  <div class="topnav" id="myTopnav" :class="{ responsive: toggle }">
    <router-link to="/">Home</router-link>
    <router-link to="/all">All Matches</router-link>
    <a href="#" class="icon" @click="toggleTopNav()">
      +
    </a>
</div>
</template>

<script>
export default {
  name: 'TopBar',
  data: function() {
    return {
      toggle: false
    };
  },
  components: {},
  methods: {
    toggleTopNav: function() {
      this.toggle = !this.toggle;
    }
  }
};
</script>

<style>
.topnav {
  overflow: hidden;
  background-color: darkred;
  margin-bottom: 20px;
}

.topnav a {
  float: left;
  display: block;
  color: #e9d9d9;
  text-align: center;
  padding: 14px 16px;
  text-decoration: none;
  font-size: 17px;
}

.topnav a:hover {
  background-color: #8f2323;
  color: e9d9d9;
}

.router-link-exact-active.router-link-active {
  background-color: #d60d0db9;
  color: white;
}

.topnav .icon {
  display: none;
}

@media screen and (max-width: 600px) {
  .topnav a:not(:first-child) {
    display: none;
  }
  .topnav a.icon {
    float: right;
    display: block;
  }
}

@media screen and (max-width: 600px) {
  .topnav.responsive {
    position: relative;
  }
  .topnav.responsive .icon {
    position: absolute;
    right: 0;
    top: 0;
  }
  .topnav.responsive a {
    float: none;
    display: block;
    text-align: left;
  }
}
</style>

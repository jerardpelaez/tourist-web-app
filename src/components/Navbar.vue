<template>
  <div>
    <v-app-bar app>
      <v-toolbar-title class="display-2 font-weight-light red--text text--lighten-3">
        <p class="nav-title ma-5">Japan Travel Guide</p>
      </v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {};
  }
};
</script>

<style>
.nav-title {
  font-family: "Gupter", serif;
  font-size: 60px;
}
@media only screen and (max-width: 600px) {
  .nav-title {
    font-size: 35px;
  }
}
</style>
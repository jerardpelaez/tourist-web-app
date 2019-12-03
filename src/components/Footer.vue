<template>
  <div>
    <v-card height="100">
      <v-footer absolute class="font-weight-medium blue lighten-4">
        <v-col class="text-center" cols="12">
          {{ new Date().getFullYear() }} —
          <strong>Vuetify</strong>
        </v-col>
      </v-footer>
    </v-card>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  }
};
</script>

<style>
</style>
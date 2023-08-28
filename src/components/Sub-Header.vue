<template>
  <v-container class="elevation-8">
    <v-row class="card">
      <v-spacer></v-spacer>
      <Search />
      <Filter />
      <v-spacer></v-spacer>
    </v-row>
  </v-container>
</template>
<script>
import Search from "@/components/Sea-rch.vue";
import Filter from "@/components/Fil-ter.vue";

export default {
  name: "App",

  components: {
    Filter,
    Search,
  },

  data: () => ({
    //
  }),
};
</script>

<style>
.card {
  font-size: 12px;
}
</style>

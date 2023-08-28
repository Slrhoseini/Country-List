<template>
  <main id="inspire">
    <Header />
    <v-row class="Subhead">
      <v-col cols="12" md="6" lg="3">
        <Search />
      </v-col>
      <v-spacer></v-spacer>
      <v-col cols="12" md="6">
        <Filter />
      </v-col>
    </v-row>
    <Countries />
  </main>
</template>

<script>
import Header from "@/components/Head-er.vue";
import Search from "@/components/Sea-rch.vue";
import Filter from "@/components/Fil-ter.vue";
import Countries from "@/components/Count-ries.vue";

import { defineComponent } from "vue";

// Components

export default defineComponent({
  name: "HomeView",

  components: { Header, Search, Filter, Countries },
});
</script>

<style>
.Subhead {
  margin-top: 2rem;
}
</style>

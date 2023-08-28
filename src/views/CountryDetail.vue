<template>
  <v-app>
    <Header />
    <v-main class="text-center d-flex justify-center align-center">
      <v-btn class="backButton" @click="goBack" prepend-icon="mdi-arrow-left">
        Back
      </v-btn>
      <v-container>
        <v-row>
          <v-col class="col1" v-if="country.flags">
            <v-img :src="country.flags.svg" alt="Flag"></v-img>
          </v-col>
          <v-col>
            <p>Capital: {{ country.capital }}</p>
            <p>Region: {{ country.region }}</p>
            <p>Population: {{ country.population }}</p>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
import { useRouter } from "vue-router";
import Header from "@/components/Head-er.vue";

export default {
  components: { Header },

  setup() {
    const router = useRouter();

    const goBack = () => {
      router.back();
    };

    return {
      goBack,
    };
  },
  data() {
    return {
      country: {},
    };
  },
  filters: {
    formatArray(array) {
      return array.join(", ");
    },
  },
  async created() {
    try {
      const countryId = this.$route.params.id;
      const response = await axios.get(
        `https://restcountries.com/v3.1/alpha/${countryId}`
      );
      this.country = response.data[0];
    } catch (error) {
      console.error("Error fetching country data:", error);
    }
  },
};
</script>

<style>
.backButton {
  margin-top: 2rem;
  margin-left: 5rem;
}
.col1 {
  background-color: red;
}
.main2 {
  background-color: yellow;
}
</style>

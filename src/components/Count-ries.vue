<template>
  <v-container>
    <v-row class="justify-space-between">
      <v-col
        v-for="(country, index) in countries"
        :key="index"
        cols="12"
        md="6"
        lg="3"
      >
        <v-card @click="goToCountryDetail(country.cca3)">
          <v-img :src="country.flags.svg" alt="Flag" height="150"></v-img>

          <v-card-title>{{ country.name.common }}</v-card-title>
          <!-- <v-card-subtitle>{{ country.region }}</v-card-subtitle> -->
          <v-card-text>
            <p>Population: {{ country.population }}</p>
            <p>Region: {{ country.region }}</p>
            <p>Capital: {{ country.capital }}</p>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  methods: {
    goToCountryDetail(countryId) {
      this.$router.push({ name: "CountryDetail", params: { id: countryId } });
    },
  },
  data() {
    return {
      countries: [],
    };
  },
  filters: {
    formatArray(array) {
      return array.join(", ");
    },
  },
  async created() {
    try {
      const response = await axios.get("https://restcountries.com/v3.1/all");
      this.countries = response.data;
    } catch (error) {
      console.error("Error fetching country data:", error);
    }
  },
};
</script>

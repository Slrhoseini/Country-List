<template>
  <v-app>
    <Header />
    <v-container>
      <v-btn class="backButton" @click="goBack" prepend-icon="mdi-arrow-left">
        Back
      </v-btn>
      <v-main class="d-flex justify-center align-center">
        <v-container>
          <v-row class="space-between">
            <v-col v-if="country.flags" cols="12" md="6" lg="6">
              <v-img
                :src="country.flags.svg"
                alt="Flag"
                height="250px"
              ></v-img>
            </v-col>
            <v-col cols="12" md="6" lg="6">
              <v-row
                ><div class="countryName mb-5">
                  <h1 v-if="country.name">{{ country.name.common }}</h1>
                </div>
                <v-col cols="12" md="6" lg="6">
                  <p class="pb-2" v-if="country.name">
                    <strong>Native Name:</strong>
                    {{ country.name.nativeName.eng.official }}
                  </p>
                  <p class="pb-2">
                    <strong>Population:</strong> {{ country.population }}
                  </p>
                  <p class="pb-2">
                    <strong>Region:</strong> {{ country.region }}
                  </p>
                  <p class="pb-2">
                    <strong>Sub Region:</strong> {{ country.subregion }}
                  </p>
                  <p class="pb-2">
                    <strong>Capital:</strong> {{ formattedCapitals }}
                  </p>
                </v-col>
                <v-col cols="12" md="6" lg="6">
                  <p class="pb-2">
                    <strong>Top Level Domain:</strong>
                    {{ country.topLevelDomain }}
                  </p>
                  <p class="pb-2">
                    <strong>Currencies:</strong> {{ formattedCurrencies }}
                  </p>
                  <p class="pb-2">
                    <strong>Languages:</strong> {{ formattedLanguages }}
                  </p>
                </v-col>
              </v-row>
            </v-col>
          </v-row>
        </v-container>
      </v-main>
    </v-container>
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
  computed: {
    formattedCapitals() {
      if (this.country.capital) {
        return this.country.capital.join(", ");
      }
      return "";
    },
    formattedCurrencies() {
      if (this.country.currencies) {
        const formattedCurrencies = [];
        for (const code in this.country.currencies) {
          const currency = this.country.currencies[code];
          const formattedCurrency = `${currency.name} (${currency.symbol})`;
          formattedCurrencies.push(formattedCurrency);
        }
        return formattedCurrencies.join(", ");
      }
      return "";
    },
    formattedLanguages() {
      if (this.country.languages) {
        const formattedLanguages = [];
        for (const code in this.country.languages) {
          const language = this.country.languages[code];
          const formattedLanguage = `${language} (${code})`;
          formattedLanguages.push(formattedLanguage);
        }
        return formattedLanguages.join(", ");
      }
      return "";
    },
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
  margin-top: 6rem;
  margin-left: 1rem;
  width: 120px;
}
.col1 {
  background-color: red;
}
.main2 {
  background-color: yellow;
}
.countryName {
  width: 100%;
}
.cored {
  background-color: red;
}
.cor2 {
  background-color: yellow;
}
</style>

<template>
  <div class="filterDiv text-center">
    <v-select
      class="filterSelect"
      :items="items"
      label="Filter by Region"
      variant="solo"
    ></v-select>
  </div>
</template>

<script>
export default {
  data: () => ({
    items: ["Africa", "America", "Asia", "Europe", "Oceania"],
  }),
};
</script>

<style>
.filterSelect {
  padding: 0 1.5rem;
  float: right;
  width: 250px;
}
/* .filterDiv {
  margin-top: 3rem;
} */
</style>

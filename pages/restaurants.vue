<template>
	<main class="container restaurant">
		<div class="restaurantheading">
			<h1>Restuarants</h1>
			<app-select @change="selectedRestaurant = $event" />
		</div>
		<!-- <app-header /> -->
		<app-restaurant-info :datasource="filteredRestaurants" />
	</main>
</template>

<script>
 // import AppHeader from "@/components/AppHeader.vue";
 import AppRestaurantInfo from "@/components/AppRestaurantInfo.vue";
 import AppSelect from "@/components/AppSelect.vue";
 import { mapState } from "vuex";

 export default{
  components: {
    // AppHeader,
    AppRestaurantInfo,
    AppSelect
  },
  data () {
    return {
      selectedRestaurant: ''
    };
  },
   computed: {
    ...mapState(["fooddata"]),
    filteredRestaurants() {
      if (this.selectedRestaurant) {
        return this.fooddata.filter((el) => {
          let name = el.name.toLowerCase();
          return name.includes(this.selectedRestaurant);
        });
      }
      return this.fooddata;
    },
  },
 };
</script>

<style>
</style>

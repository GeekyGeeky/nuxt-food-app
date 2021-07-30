<template>
	<main class="container">
		<app-header />
		<app-restaurant-info :datasource="fooddata" />
	</main>
</template>

<script>
 import AppHeader from "@/components/AppHeader.vue";
 import AppRestaurantInfo from "@/components/AppRestaurantInfo.vue";
 
 export default{
  components: {
    AppHeader,
    AppRestaurantInfo,
  },
   computed: {
    fooddata() {
      return this.$store.state.fooddata;
    },
  },
 }
</script>

<style>
</style>

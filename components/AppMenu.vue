<template>
	<nav>
		<ul>
			<li>
				<nuxt-link exact to="/"> <app-logo /> </nuxt-link>
			</li>
			<li><nuxt-link to="/restaurants"> Restaurants </nuxt-link></li>
		</ul>
		<div class="smallnum" v-show="countCartItems > 0">{{ countCartItems }}</div>
		<nuxt-link to="/cart">Cart</nuxt-link>
	</nav>
</template>

<script>
  import AppLogo from '@/components/AppLogo.vue';
  import { mapGetters } from 'vuex'
  
  export default{
 components:{
  AppLogo
 },
 computed:{
      ...mapGetters(["countCartItems"])
  },
}
</script>

<style lang="scss" scoped>
</style>
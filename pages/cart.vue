<template>
	<main class="container cart">
		<h2>Cart</h2>
		<section v-if="cart.length">
			<table>
				<thead>
					<tr>
						<th>Item</th>
						<th>Add Ons</th>
						<th>Amount</th>
						<th>Total Price</th>
					</tr>
				</thead>
				<tbody>
					<tr v-for="item in cart" :key="item.id">
						<td>
							{{ item.item }}
							<span v-if="item.options"
								>- {{ item.options }}</span
							>
						</td>
						<td>
							<span
								v-for="addon in item.addOns"
								:key="addon"
								class="comma"
								>{{ addon }}</span
							>
							<span v-if="!item.addOns.length">Nil</span>
						</td>
						<td>{{ item.numberOfItems }}</td>
						<td>{{ item.totalPrice }}</td>
					</tr>
					<tr>
						<td colspan="3"></td>
						<td class="total">
							Total: ${{ totalPrice.toFixed(2) }}
						</td>
					</tr>
				</tbody>
			</table>
		</section>
    <app-empty-cart v-else />
	</main>
</template>

<script>
	import { mapState, mapGetters } from 'vuex';
  import AppEmptyCart from '@/components/AppEmptyCart.vue'
	
	export default{
  components:{
    AppEmptyCart
  },
  computed:{
			...mapState(["cart"]),
      ...mapGetters(['totalPrice'])
      // totalPrice(){
      //   // if(!this.cart.length) return 0;
      //   // return this.cart.reduce((initial, next) => initial + +next.totalPrice, 0);
      //   let total = 0;
      //   this.cart.forEach((cartData)=>{
      //     total += Number(cartData.totalPrice);
      //   });
      //   return total;
      // }
		},
}
</script>

<style lang="scss" scoped>
</style>
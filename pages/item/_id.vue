<template>
	<main class="container">
		<section
			class="image"
			:style="`background: url(/${currentItem.img}) no-repeat center center;`"
		></section>
		<section class="details">
			<h2>
				{{ currentItem.item }}
			</h2>
			<h4>Price: {{ formatPrice }}</h4>
			<div class="quantity">
				<input
					type="number"
					min="1"
					max="100"
					v-model="numberOfItems"
				/>
				<button @click="addToCart" class="primary">
					Add to cart - {{ totalPrice }}
				</button>
			</div>
			<fieldset v-if="currentItem.options">
				<legend><h3>Options</h3></legend>
				<div v-for="option in currentItem.options" :key="option">
					<input
						type="radio"
						:value="option"
						v-model="itemOptions"
						:id="option"
						name="option"
					/>
					<label :for="option">{{ option }}</label>
				</div>
			</fieldset>
			<fieldset v-if="currentItem.addOns">
				<legend><h3>Add Ons</h3></legend>
				<div v-for="addon in currentItem.addOns" :key="addon">
					<input
						type="checkbox"
						:value="addon"
						v-model="addons"
						:id="addon"
						name="addon"
					/>
					<label :for="addon">{{ addon }}</label>
				</div>
			</fieldset>
			<app-toast v-show="cartSubmitted">
				Order submitted <br />
				Check out more
				<nuxt-link to="/restaurants">restaurants</nuxt-link>
			</app-toast>
		</section>
		<section class="options">
			<h2>Description</h2>
			<p>{{ currentItem.description }}</p>
		</section>
	</main>
</template>

<script>
import { mapState } from 'vuex'
import AppToast from '@/components/AppToast.vue';

export default{
  components:{
    AppToast
  },
  data () {
    return {
    	id: this.$route.params.id,
      numberOfItems: 1,
      addons: [],
      itemOptions: '',
      itemSizeAndCost: [],
      cartSubmitted:false
    }
  }, 
  computed:{
		...mapState(['fooddata']),
		currentItem(){
			let result;
      for (let i = 0; i < this.fooddata.length; i++) {
        for (let j = 0; j < this.fooddata[i].menu.length; j++) {
          let foodData = this.fooddata[i].menu[j];
          if(foodData.id === this.id){
            result = foodData;
            break;
          }
        }
      }
      return result;
		},
    formatPrice(){
      if(!this.currentItem) return '';
      return '$' + this.currentItem.price.toFixed(2);
    },
    totalPrice(){
      if(!this.currentItem) return 0;
      // if(!this.currentItem) return this.currentItem.price;
      return '$' + (this.numberOfItems * this.currentItem.price).toFixed(2);
    }
	},
  methods: {
    addToCart () {
      let formOptions = {
        item: this.currentItem.item,
        numberOfItems: this.numberOfItems,
        options: this.itemOptions,
        addOns: this.addons,
        totalPrice: (this.numberOfItems * this.currentItem.price).toFixed(2)
      };
      this.cartSubmitted = true;
      this.$store.commit('addToCart', formOptions);
    }
  }
}
</script>

<style lang="css" scoped>
.container {
	width: 1000px;
	margin: 100px auto;
	display: grid;
	grid-template-columns: 400px 1fr;
	grid-template-rows: 400px 1fr;
	grid-column-gap: 60px;
	grid-row-gap: 60px;
	line-height: 2;
}
.image {
	grid-area: 1 / 1 / 2 / 2;
	background-size: cover;
}
.details {
	grid-area: 1 / 2 / 2 / 3;
	position: relative;
}
.options {
	grid-area: 2 / 1 / 3 / 2;
}
</style>
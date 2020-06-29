<script>
export default {
	name: "MenuItem",
	props: ["addToShoppingCart", "image", "inStock", "name", "price", "quantity"],
	//beforeCreate() { console.log('beforeCreate') },
	//created() { console.log('created ! '+this.name) },
	data(){
		return{
			reduction : false
		}
	},
	beforeMount() { 
		let date = new Date().getDate()
		if((date % 2) == 0){
			console.log('beforeMount date : '+date+' '+this.name);
			this.reduction = false;
		}else{
			this.reduction = true;
		}
		
	},
	computed:{
		generatedPrice(){
			if(this.reduction){
				return (this.price * 0.9).toFixed(2);
			}else{
				return this.price;
			}
		}
	}
	//mounted() { console.log('mounted '+this.name) },
	//beforeDestroy() { console.log('beforeDestroy '+this.name) },
	//destroyed() { console.log('destroyed '+this.name) }
}
</script>

<template>
	<div class="menu-item">
		<img class="menu-item__image" :src="image.source" :alt="image.alt" />
		<div>
			<h3>{{ name }}</h3>
			<p>Prix : {{ generatedPrice }}</p>
			<p v-if="inStock">En stock</p>
			<p v-else>En rupture de stock</p>
			<div>
				<label for="add-item-quantity">Quantité : {{ quantity }}</label>
				<input v-model.number="quantity" id="add-item-quantity" type="number" />
				<button @click="addToShoppingCart(quantity)">
					Ajouter au panier
				</button>
			</div>
		</div>
	</div>
</template>

<style></style>

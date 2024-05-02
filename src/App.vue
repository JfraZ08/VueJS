<template>
	<div id="app" class="app">
		<h1>{{ restaurantName }}</h1> <!--affichage du nom du restaurant au format dynamique-->
		<p class="description">
			Bienvenue dans notre café {{ restaurantName }}! Nous sommes réputés pour
			notre pain et nos merveilleuses pâtisseries. Faites vous plaisir dès le
			matin ou avec un goûter réconfortant. Mais attention, vous verrez qu'il
			est difficile de s'arrêter.
		</p>

		<section class="menu">
			<h2>Menu</h2>
			<MenuItem
				v-for="item in simpleMenu"
				:addToShoppingCart="addToShoppingCart"
				:name="item.name"
				:image="item.image"
				:quantity="item.quantity"
				:inStock="item.inStock"
				:key="item.name"
			/><!--condition for pour affiche tout les items du menu via des v-bind de menuItem-->
		</section>

		<aside class="shopping-cart">
			<h2>Panier d'achat : {{ shoppingCart }} articles</h2><!--affichage du total du panier au format dynamique-->
		</aside>

		<h2>Contactez nous</h2>
		<p>Adresse : {{ address }}</p><!--affichage adresse restaurant au format dynamique-->
		<p>Téléphone : {{ phone }}</p><!--affichage telephone restaurant au format dynamique-->
		<p>Email : {{ email }}</p><!--affichage mail du restaurant au format dynamique-->
		<p>Horaires :</p>
		<ul>
			<li>L-V: 06:00 à 16:00</li>
			<li>Samedi: 07:00 à 14:00</li>
			<li>Dimanche: 07:00 à 12:00</li>
		</ul>
		<footer class="footer">
			<p>{{ copyright }}</p><!--affichage du copyright et de l'aannée au format dynamique-->
		</footer>
	</div>
</template>

<script>
import MenuItem from "./components/MenuItem"

export default {
	name: "App",
	components: {
		MenuItem
	},
	data() {
		return {
			address: "18 avenue du Beurre, Paris, France",
			email: "hello@cafewithavue.bakery",
			phone: "01 88 88 88 88",
			restaurantName: "La belle vue",
			shoppingCart: 0,
			simpleMenu: [//liste d'item sous tableau de simpleMenu
				{
					name: "Croissant",
					image: {
						source: "/images/croissant.jpg",
						alt: "Un croissant"
					},
					inStock: true, // en stock sous fotmat boolean
					quantity: 1
				},
				{
					name: "Baguette de pain",
					image: {
						source: "/images/french-baguette.jpeg",
						alt: "Quatre baguettes de pain"
					},
					inStock: true,
					quantity: 1
				},
				{
					name: "Éclair",
					image: {
						source: "/images/eclair.jpg",
						alt: "Éclair au chocolat"
					},
					inStock: false, // en rupture de sotck sous format boolean
					quantity: 1
				}
			]
		}
	},
	computed: {
		copyright() {
			const currentYear = new Date().getFullYear() // Date au format année seulement

			return `Copyright ${this.restaurantName} ${currentYear}` // Copyright + nomResto + Année en cours
		}
	},
	methods: {
		addToShoppingCart(amount) {
			this.shoppingCart += amount
		} // ajout pour panier
	}
}
</script>

<style lang="scss">
#app {
	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
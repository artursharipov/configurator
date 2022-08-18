<template>
	<div class="carconfig">
		<div class="x-row">
			<div class="x-col-60">

				<car-image src="toyota/white/disk2.png">

				</car-image>

				<div class="carconfig__price">
					{{ calcPrice }}
				</div>

			</div>
			<div class="x-col-40">

				<div class="properties">

					<div class="property">
						<div class="property__title">ОБЪЁМ ДВИГАТЕЛЯ</div>

						<switch-button 
							v-for="engine in engines" 
							:key="engine.id"
							@click="engineActive=engine.id" 
							:class="{active: engineActive == engine.id}"
						>{{ engine.name }}</switch-button>

					</div>

					<div class="property">
						<div class="property__title">КОРОБКА ПЕРЕДАЧ</div>

						<switch-button 
							v-for="transmission in transmissions" 
							:key="transmission.id"
							@click="transmissionActive=transmission.id" 
							:class="{active: transmissionActive == transmission.id}"
						>{{ transmission.name }}</switch-button>

					</div>

				</div>

			</div>
		</div>
	</div>
</template>

<script>
import CarImage from './components/CarImage.vue'
import SwitchButton from './components/SwitchButton.vue'

export default {
	name: 'App',
	components: {
		CarImage,
		SwitchButton
	},
	data(){
		return {
			basePrice: 1000,
			engineActive: 2,
			transmissionActive: 2,
			engines: [
				{id: 1, name: "2.8 л", price: 300},
				{id: 2, name: "3.0 л", price: 400},
				{id: 3, name: "3.5 л", price: 500},
			],
			transmissions: [
				{id: 1, name: "MT", price: 40},
				{id: 2, name: "AT", price: 70},
				{id: 3, name: "CVT", price: 80},
			]
		}
	},
	computed: {
		calcPrice(){
			let engine = this.engines.find(item => item.id == this.engineActive);
			let transmission = this.transmissions.find(item => item.id == this.transmissionActive);
			return this.basePrice + engine.price + transmission.price;
		}
	}
}
</script>

<style>
.carconfig{
	background-color: #252525;
	color: #fff;
	height: 100vh;
	width: 100%;
}
.x-row{
	display: flex;
	align-items: center;
	justify-content: center;
}
.x-col-60{
	flex: 1 1 60%;
}
.x-col-40{
	flex: 1 1 40%;
}
.property{
	margin-bottom: 20px;
}
.property__title{
	margin-bottom: 10px;
}
</style>

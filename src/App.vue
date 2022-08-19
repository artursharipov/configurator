<template>
	<div class="carconfig">
		<div class="x-row">
			<div class="x-col-60">

				<car-image :src="src">

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

					<div class="property">
						<div class="property__title">Цвет кузова</div>

						<check-button 
							v-for="color in colors" 
							:key="color.id"
							@click="colorActive=color.id, changeSrc()" 
							:class="[{active: colorActive == color.id}, color.colorName]"
						></check-button>

					</div>

					<div class="property">
						<div class="property__title">Цвет кузова</div>

						<image-button 
							v-for="disk in disks" 
							:key="disk.id"
							@click="diskActive=disk.id, changeSrc()" 
							:class="[{active: diskActive == disk.id}]"
							:src="disk.src"
						></image-button>

					</div>

					<div class="property">
						<div class="property__title">Дефлекторы окон и капота</div>

						<switch-button 							
							@click="deflector = true, changeSrc()" 
							:class="{active: deflector == true}"
						>Да</switch-button>

						<switch-button 							
							@click="deflector = false, changeSrc()" 
							:class="{active: deflector == false}"
						>Нет</switch-button>

					</div>

				</div>

			</div>
		</div>
	</div>
</template>

<script>
import CarImage from './components/CarImage.vue'
import SwitchButton from './components/SwitchButton.vue'
import CheckButton from './components/CheckButton.vue'
import ImageButton from './components/ImageButton.vue'

export default {
	name: 'App',
	components: {
		CarImage,
		SwitchButton,
		CheckButton,
		ImageButton
	},
	data(){
		return {
			basePrice: 1000,
			src: null,
			engineActive: 2,
			transmissionActive: 2,
			colorActive: 1,
			diskActive: 1,
			deflector: false,
			engines: [
				{id: 1, name: "2.8 л", price: 300},
				{id: 2, name: "3.0 л", price: 400},
				{id: 3, name: "3.5 л", price: 500},
			],
			transmissions: [
				{id: 1, name: "MT", price: 40},
				{id: 2, name: "AT", price: 70},
				{id: 3, name: "CVT", price: 80},
			],
			colors: [
				{id: 1, name: "Белый", colorName: 'white', price: 36},
				{id: 2, name: "Красный", colorName: 'red', price: 42},
				{id: 3, name: "Синий", colorName: 'blue', price: 41},
				{id: 4, name: "Серый", colorName: 'darkgray', price: 39},
			],
			disks: [
				{id: 1, name: "disk1", src: 'toyota/disk1.png', price: 14},
				{id: 2, name: "disk2", src: 'toyota/disk2.png', price: 12},
			],
		}
	},
	computed: {
		calcPrice(){
			let engine = this.engines.find(item => item.id == this.engineActive);
			let transmission = this.transmissions.find(item => item.id == this.transmissionActive);
			let color = this.colors.find(item => item.id == this.colorActive);
			let disk = this.disks.find(item => item.id == this.diskActive);
			return this.basePrice + engine.price + transmission.price + color.price + disk.price;
		},
	},
	methods: {
		changeSrc(){
			let color = this.colors.find(item => item.id == this.colorActive);
			let disk = this.disks.find(item => item.id == this.diskActive);
			let deflectorString = this.deflector ? '+defl' : '';
			
			this.src = 'toyota/'+ color.colorName +'/'+ disk.name + deflectorString + '.png'
		}
	},
	mounted() {
		this.changeSrc();
	}

}
</script>

<style scoped>
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

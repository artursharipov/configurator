<template>
	<div class="carconfig">
		<div class="uk-grid" uk-grid>
			<div class="uk-width-2-3@l uk-width-1-2@m ">

				<div class="carconfig__container">

					<car-image :src="src"></car-image>
					
					
				</div>

				<div class="result">
					<div class="result__content">
						<car-image :src="srcSalon" class="salon-image"></car-image>

						<div class="carconfig__price">
							{{ calcPrice }} руб.
						</div>
					</div>
				</div>
				

			</div>
			<div class="uk-width-1-3@l uk-width-1-2@m">

				<div class="properties">

					<div class="property">
						<div class="property__title">Комплектация</div>

						<switch-button 
							v-for="engine in engines" 
							:key="engine.id"
							@click="engineActive=engine.id" 
							:class="{active: engineActive == engine.id}"
						>{{ engine.name }}</switch-button>

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

					<div class="property">
						<div class="property__title">Интерьер</div>

						<image-button 
							v-for="salon in salons" 
							:key="salon.id"
							@click="salonActive=salon.id, changeSalonSrc()" 
							:class="[{active: salonActive == salon.id}]"
							:src="salon.thumb"
						></image-button>

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
			srcSalon: null,
			engineActive: 2,
			colorActive: 1,
			salonActive: 1,
			diskActive: 1,
			deflector: false,
			deflectorPrice: 10500,
			engines: [
				{id: 1, name: "Стандарт", price: 2498000},
				{id: 2, name: "Престиж", price: 2678000},
				{id: 3, name: "Эксклюзив", price: 2805000},
			],
			colors: [
				{id: 1, name: "Белый", colorName: 'white', price: 100800},
				{id: 2, name: "Красный", colorName: 'red', price: 130600},
				{id: 3, name: "Синий", colorName: 'blue', price: 113900},
				{id: 4, name: "Серый", colorName: 'darkgray', price: 125700},
			],
			disks: [
				{id: 1, name: "disk1", src: '/vue/configurator/dist/toyota/disk1.png', price: 100000},
				{id: 2, name: "disk2", src: '/vue/configurator/dist/toyota/disk2.png', price: 200000},
			],
			salons: [
				{id: 1, thumb: '/vue/configurator/dist/salon/thumb1.png', price: 70000},
				{id: 2, thumb: '/vue/configurator/dist/salon/thumb2.png', price: 115000},
			]
		}
	},
	computed: {
		calcPrice(){
			let engine = this.engines.find(item => item.id == this.engineActive);
			let color = this.colors.find(item => item.id == this.colorActive);
			let disk = this.disks.find(item => item.id == this.diskActive);
			let defl = this.deflector ? this.deflectorPrice : 0;
			let cost = this.basePrice + engine.price + color.price + disk.price + defl;
			return cost.toString().replace(/(\d)(?=(\d{3})+$)/g, '$1 ')
		},
	},
	methods: {
		changeSrc(){
			let color = this.colors.find(item => item.id == this.colorActive);
			let disk = this.disks.find(item => item.id == this.diskActive);
			let deflectorString = this.deflector ? '+defl' : '';
			
			this.src = '/vue/configurator/dist/toyota/'+ color.colorName +'/'+ disk.name + deflectorString + '.png'
		},
		changeSalonSrc(){
			this.srcSalon = '/vue/configurator/dist/salon/'+ this.salonActive +'.jpg'
		}
	},
	mounted() {
		this.changeSrc();
		this.changeSalonSrc();
	}

}
</script>

<style scoped>
.carconfig__container img{
	max-width: 100%;
}
.result{
	padding: 15px;
}
.result__content{
	display: flex;
    align-items: center;
    justify-content: center;
}
.salon-image{
	width: 250px;
	margin-right: 20px;
}
.carconfig__price{
	font-size: 32px;
	font-weight: 600;
    text-align: center;
	white-space: nowrap;
}
.properties{
	text-align: center;
}
.property{
	padding: 13px 10px;
}
.property__title{
	color: #9b9b9b;
    text-align: center;
    text-transform: uppercase;
    font-weight: 700;
    margin-bottom: 15px;
}
</style>

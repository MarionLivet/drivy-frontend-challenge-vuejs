<template>
<div class="cars-list">
  <div class="cars-list-form">
    <label class="cars-list-label" htmlFor="distance">
      <span>Distance (in km)</span>
      <input
        class="cars-list-input"
        id="distance"
        type="number"
        v-model="distance"
        max="3000"
        min="0"
      />
    </label>
    <label class="cars-list-label" htmlFor="duration">
      <span>Duration (in days)</span>
      <input
        class="cars-list-input"
        id="duration"
        type="number"
        v-model="duration"
        max="30"
        min="1"
      />
    </label>
  </div>
  <div class="cars-list-content">
    <Car v-for="car in carsWithPrice" :car="car" :key="car.id" />
  </div>
</div>
</template>

<script>
import Car from './Car';
import getCarPrice from '../logic/getCarPrice';

export default {
  data() {
    return {
      duration: '2',
      distance: '100',
      cars: [],
    };
  },
	components: {
    Car,
	},
  computed: {
    carsWithPrice: function () {
      return this.cars.map((car) => ({
        ...car,
        price: getCarPrice(this.distance, this.duration, car),
      }));
    },
  },
  methods: {
    getCarsData: function() {
      return fetch('http://localhost:3001/cars.json?distance=' + this.distance + '&duration=' + this.duration)
        .then((res) => res.json())
        .then((json) => this.cars = json);
    },
  },
  watch: {
    distance: {
      immediate: true,
      handler() {
        this.getCarsData()
      },
    },
    duration: {
      immediate: false,
      handler() {
        this.getCarsData()
      },
    },
  },
}
</script>

<style>
.cars-list-form {
  max-width: 1200px;
  margin: 40px auto;
  padding: 0 12px;
  background: #f7f9f9;
  border-radius: 5px;
  padding: 10px 20px;
  box-sizing: border-box;
}

.cars-list-input {
  background: #f7f9f9;
  flex: 1;
  border-radius: 5px;
  padding: 5px 8px;
  border: 1px solid #e2e2e2;
  font-size: 18px;
  transition: border 300ms ease;
}
.cars-list-input:hover {
  border: 1px solid #c3c3c3;
}

.cars-list-label {
  display: flex;
  margin: 5px 0;
  font-size: 18px;
}
.cars-list-label span {
  min-width: 20%;
}

.cars-list-content {
  max-width: 1200px;
  margin:  0 auto 80px auto;
  padding: 0 12px;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 10px;
}

@media(max-width: 880px) {
  .cars-wrapper {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media(max-width: 460px) {
  .cars-wrapper {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
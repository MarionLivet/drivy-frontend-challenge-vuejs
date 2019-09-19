<template>
<div id="app">
  <header class="header">
    <img class="logo" src="https://d2y2masl4rtrav.cloudfront.net/packs/images/shared/drivy-by-ga-logo-9eaed4df8ac81b13add18d2d06aa2272.svg" alt="Drivy" />
  </header>
  <CarsList />
</div>
</template>

<script>
import CarsList from './components/CarsList.vue';

export default {
	components: {
    CarsList,
	},
}
</script>

<style>
body {
  padding: 0;
  margin: 0;
  font-family: 'Noto Sans KR', sans-serif;
}

.header {
  position: sticky;
  top: 0;
  background: white;
  padding: 12px 20px;
  border-bottom: 1px solid #e2e2e2;
  z-index: 10;
}

.logo {
  display: block;
  margin: auto;
}
</style>
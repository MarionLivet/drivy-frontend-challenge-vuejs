<template>
<a class="car" href="#">
  <img class="car-picture" :src="'http://localhost:3001/' + car.picturePath" :alt="car.model" />
  <div class="car-content">
    <div class="car-title"><span>{{car.brand}} {{car.model}}</span></div>
    <div class="car-price">{{car.price}}€</div>
  </div>
</a>
</template>

<script>
export default {
  props: ['car'],
}
</script>

<style>
.car {
  display: flex;
  flex-direction: column;
  color: #333;
  text-decoration: none;
  border-radius: 5px;
  overflow: hidden;
}

.car-picture {
  display: block;
  max-width: 100%;
}

.car-content {
  position: relative;
  padding: 10px 20px;
  background: #f7f9f9;
  transition: 300ms ease background;
}
.car:hover .car-content {
  background: #f1f5f5;
}

.car-title {
  position: relative;
  display: inline-block;
  font-size: 18px;
  font-weight: 500;
  color: #262959;
}
.car-title span {
  position: relative;
}
.car-title::before {
  content: "";
  position: absolute;
  bottom: 0;
  left: 0;
  display: block;
  width: 100%;
  height: 0;
  background: #00d9d9;
  transition: 300ms ease height;
}
.car:hover .car-title::before {
  height: 10px;
}

.car-price {
  position: absolute;
  right: 0;
  top: -50px;
  padding: 4px 16px 9px 16px;
  background: #50588c;
  font-size: 20px;
  color: #fff;
  transform: translateX(5px);
  transition: transform 300ms ease;
}
.car:hover .car-price {
  transform: translateX(0);
}
</style>
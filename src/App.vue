<script setup>
import { reactive, computed } from "vue";

const categories = reactive({
  Drinks: {
    name: "المشروبات",
    active: true,
  },
  Food: {
    name: "الاكل",
    active: false,
  },
});

const Products = reactive({
  Drinks: [
    {
      name: "Espresso",
      img: "https://www.tasteofhome.com/wp-content/uploads/2023/02/TOH-coffee-vs-espresso-GettyImages-1413384122-JVedit.jpg",
      price: "30",
    },
    {
      name: "Black Coffee",
      img: "https://media.cnn.com/api/v1/images/stellar/prod/150929101049-black-coffee-stock.jpg?q=w_3000,h_3074,x_0,y_0,c_fill",
      price: "25",
    },
    {
      name: "Latte",
      img: "https://www.tasteofhome.com/wp-content/uploads/2023/02/TOH-coffee-vs-espresso-GettyImages-1413384122-JVedit.jpg",
      price: "35",
    },
  ],
  Food: [
    {
      name: "Burger",
      img: "https://simplehomeedit.com/wp-content/uploads/2024/03/Homemade-Beef-Burgers-4.webp",
      price: "50",
    },
    {
      name: "Pizza",
      img: "https://www.allrecipes.com/thmb/fFW1o307WSqFFYQ3-QXYVpnFj6E=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/48727-Mikes-homemade-pizza-DDMFS-beauty-4x3-BG-2974-a7a9842c14e34ca699f3b7d7143256cf.jpg",
      price: "75",
    },
    {
      name: "Pasta",
      img: "https://food.fnr.sndimg.com/content/dam/images/food/fullset/2021/02/05/Baked-Feta-Pasta-4_s4x3.jpg.rend.hgtvcom.1280.1280.suffix/1615916524567.jpeg",
      price: "60",
    },
  ],
});

function setCategoryActive(name) {
  // Set all categories to inactive
  for (const key in categories) {
    categories[key].active = false;
  }

  // Set the specified category to active
  if (categories[name]) {
    categories[name].active = true;
  }
}

const activeProducts = computed(() => {
  const activeCategory = Object.keys(categories).find((key) => categories[key].active);
  return Products[activeCategory] || [];
});
</script>

<template>
  <header class="flex items-center justify-between md:mt-12 max-md:flex-col max-md:justify-center max-md:gap-y-5">
    <div class="flex flex-col items-center justify-center w-full">
      <h1 class="text-3xl font-bold text-gray-50">Lido Coffee.</h1>
      <p class="px-5 text-center mt-2.5 text-gray-200">Where taste, beauty, tranquility and peace of mind with a cup of coffee from the purest beans make life meaningful</p>
    </div>
    <div class="flex items-center justify-center w-full max-md:-order-1">
      <img src="./assets/logo.png" alt="logo" class="h-80" />
    </div>
  </header>
  <main>
    <div class="flex flex-col items-center justify-center">
      <h1 class="my-5 text-3xl font-medium text-white">الاقسام</h1>
      <ul class="flex items-center justify-between gap-x-5">
        <li v-for="(category, key) in categories" :key="key" @click="setCategoryActive(key)" :class="{ 'border-b-4 ': category.active }" class="rounded-lg">
          <button class="px-5 py-2 text-white rounded-lg">
            {{ category.name }}
          </button>
        </li>
      </ul>
    </div>
    <transition-group name="fade" tag="div" class="container grid grid-cols-12 gap-2 mx-auto my-8 max-md:grid-cols-4 px-2.5">
      <div v-for="product in activeProducts" :key="product.name" class="col-span-2 p-2 rounded-lg shadow-lg bg-neutral-800">
        <img class="w-full rounded-lg size-40" :src="product.img" :alt="product.name" />
        <h2 class="pt-2 text-lg font-medium text-white">{{ product.name }}</h2>
        <h3>
          <span class="text-xl font-medium text-gray-200 pe-1">{{ product.price }}</span>
          <span class="text-gray-300">EG</span>
        </h3>
      </div>
    </transition-group>
  </main>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.4s ease, transform 0.4s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(20px);
}
.fade-enter-to,
.fade-leave-from {
  opacity: 1;
  transform: translateY(0);
}
</style>

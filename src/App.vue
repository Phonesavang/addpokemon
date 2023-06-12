<script setup>
import Favorites from "./components/Favorites.vue";
import { ref, watchEffect } from "vue";
const data = ref([]);
const item = ref([]);
const id = ref(1);
const getData = async () => {
  await fetch(`https://pokeapi.co/api/v2/pokemon/${id.value}`)
    .then((rep) => rep.json())
    .then((elm) => (data.value = elm));
};
const adItem = (data) => {
  item.value = data;
};
watchEffect(() => {
  getData();
});
</script>

<template>
  <div class="h-[100vh] sm:flex items-center justify-center box bg-slate-200">
    <div
      class="grid sm:grid-cols-2 p-5 sm:p-0 h-auto sm:h-[470px] border-slate-600 rounded-md border-2 bg-slate-100"
    >
      <div
        class="p-5 sm:h-[470px] text-center border-b-2 sm:border-b-0 sm:border-r-2 border-slate-600"
      >
        <h1 class="font-bold text-2xl">{{ data?.name }}</h1>
        <img
          class="h-[250px] mx-auto"
          :src="data?.sprites?.other?.home.front_default"
          :alt="data?.name"
        />
        <ul>
          <li v-for="(item, idx) in data?.abilities" :key="idx">
            {{ item?.ability.name }}
          </li>
        </ul>
        <button
          @click="adItem(data)"
          style="transition: ease-in-out 0.3s"
          class="mt-3 hover:bg-pink-600 hover:text-white border-2 text-pink-600 border-pink-400 text-lg w-24 h-8 border rounded-md"
        >
          Like
        </button>
        <div class="flex items-center justify-center gap-8">
          <button
            @click="id--"
            style="transition: ease-in-out 0.3s"
            class="mt-3 hover:bg-cyan-600 hover:text-white text-cyan-900 border-2 text-sm border-cyan-400 text-lg w-[7rem] h-8 border rounded-md"
          >
            retrospective
          </button>
          <button
            @click="id++"
            style="transition: ease-in-out 0.3s"
            class="mt-3 hover:bg-cyan-600 hover:text-white text-cyan-900 border-2 text-sm border-cyan-400 text-lg w-[4rem] h-8 border rounded-md"
          >
            Next
          </button>
        </div>
      </div>
      <Favorites :dataItem="item" />
    </div>
  </div>
</template>
<style>
@media only screen and (max-width: 580px) {
  .box {
    height: auto;
  }
}
</style>

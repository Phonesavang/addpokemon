<script setup>
import { ref, watch } from "vue";
const props = defineProps(["dataItem"]);
const datas = ref([]);
const sum = ref(0);
watch(props, () => {
  datas.value.push(props.dataItem);
  sum.value = datas.value.length;
});
const del = (id) => {
  const newData = datas.value.filter((elm) => elm.id != id);
  datas.value = newData;
  sum.value = datas.value.length;
};
const setValue = () => {
  datas.value = [];
  sum.value = datas.value.length;
};
</script>

<template>
  <div class="sm:w-[25rem] sm:h-[470px] overflow-y-auto p-5">
    <div class="flex items-center justify-between">
      <h1 class="font-bold text-2xl">Favorites ({{ sum }})</h1>
      <button
        @click="setValue"
        class="bg-red-600 text-white w-16 rounded active:bg-red-500"
      >
        Clear
      </button>
    </div>
    <div class="grid grid-cols-5 mt-5 sm:grid-cols-4 gap-2">
      <div
        class="relative text-center bg-white border rounded-md shadow-md"
        v-for="data in datas"
        :key="data.id"
      >
        <h4 class="text-[12px]">{{ data.name }}</h4>
        <img
          class="h-20 mx-auto"
          :src="data?.sprites?.other?.home.front_default"
          alt=""
        />
        <span @click="del(data.id)" class="icon">X</span>
      </div>
    </div>
  </div>
</template>
<style scoped>
.icon {
  position: absolute;
  top: -6px;
  right: -6px;
  background-color: red;
  height: 17px;
  width: 17px;
  border-radius: 50%;
  color: #fff;
  font-size: 12px;
  cursor: pointer;
}
</style>
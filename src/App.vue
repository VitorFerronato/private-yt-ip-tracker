<template>
  <div class="flex flex-col h-screen max-h-screen">
    <div
      class="z-20 flex justify-center bg-[#253342] relative bg-cover px-4 pt-8 pb-32"
    >
      <div class="w-full max-w-screen-sm">
        <h1 class="text-white text-center text-3xl pb-4">IP Adress Tracker</h1>

        <Input-Search @handleGetIpInfo="getIpInfo" />
      </div>

      <Ip-Info v-if="ipInfo" :ipInfo="ipInfo" />
    </div>

    <div id="map" class="h-full z-10"></div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import L from "leaflet";
import axios from "axios";
import IpInfo from "@components/IpInfo.vue";
import InputSearch from "@components/InputSearch.vue";

let myMap;
const ipInfo = ref(null);

const getIpInfo = async (queryIp) => {
  console.log(queryIp);
  try {
    const { data } = await axios.get(`http://ip-api.com/json/${queryIp}`);

    ipInfo.value = {
      address: data.query,
      state: data.country,
      timezone: data.timezone,
      isp: data.isp,
      lat: data.lat,
      lon: data.lon,
    };

    L.marker([ipInfo.value.lat, ipInfo.value.lon]).addTo(myMap);
    myMap.setView([ipInfo.value.lat, ipInfo.value.lon], 11);
  } catch (error) {
    alert(`Erro ao buscar informações do IP: ${error.message}`);
  }
};

onMounted(() => {
  myMap = L.map("map").setView([51.505, -0.09], 9);

  L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
    maxZoom: 19,
    attribution:
      '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
  }).addTo(myMap);
});
</script>

<template>
  <div class="flex">
    <input
      v-model="queryIp"
      class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md focus:outline-none"
      placeholder="Search for any IP address or leave empty to get your ip info"
      type="text"
    />
    <i
      @click="() => emit('handleGetIpInfo', queryIp)"
      class="cursor-pointer bg-[#34485d] text-white px-4 rounded-tr-md rounded-br-md flex items-center fa-solid fa-chevron-right"
    ></i>
  </div>
</template>

<script setup>
import { ref } from "vue";

const emit = defineEmits(["handleGetIpInfo"]);
const queryIp = ref("");
</script>

<template>
  <div
    class="absolute -bottom-64 lg:-bottom-20 flex fle-col lg:flex-row bg-white gap-y-4 gap-x-12 px-8 pt-8 pb-12 rouded-md"
  >
    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">IP Address</h3>
      <span class="text-2xl">{{ ipInfo.address }}</span>
    </div>

    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">Location</h3>
      <span class="text-2xl">{{ ipInfo.state }}</span>
    </div>

    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">Timezone</h3>
      <span class="text-2xl">{{ ipInfo.timezone }}</span>
    </div>

    <div class="flex flex-col">
      <h3 class="text-xs mb-2 uppercase">Isp</h3>
      <span class="text-2xl">{{ ipInfo.isp }}</span>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  ipInfo: {
    type: Object,
  },
});
</script>

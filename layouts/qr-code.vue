<script setup lang="ts">
import { computed } from "vue";
import QRious  from "qrious";

const url = window.location.href.replace(/\/[^\/]*$/, "/");

const qrcode = computed(() => {
  return new QRious({
    value: url,
    size: 300,
  }).toDataURL();
});
</script>

<template>
  <div class="slidev-layout qrcode text-center">
    <slot />
    <div class="container mx-auto mt-8">
      <img :src="qrcode" alt="QR Code" class="inline-block" />
    </div>
  </div>
</template>

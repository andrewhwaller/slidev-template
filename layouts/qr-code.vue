<script setup lang="ts">
import { computed } from "vue";
import { useRouter } from "vue-router";
import QRious  from "qrious";

const router = useRouter();
const route = router.resolve({
  path: "/",
})
const url = window.location.origin + route.href;

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

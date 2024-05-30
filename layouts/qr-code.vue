<script setup lang="ts">
import { computed, onMounted } from "vue";
import QRCodeStyling from "qr-code-styling";

const url = window.location.href.replace(/\/presenter|\/[^\/]*$/, "/");

const qrcode = computed(() => {
  return new QRCodeStyling({
    width: 300,
    height: 300,
    type: "svg",
    data: url,
    dotsOptions: {
      color: "#000000",
      type: "classy-rounded",
    },
    backgroundOptions: {
      color: "#ffffff",
    },
  })
});

onMounted(() => {
  document.getElementById("qrContainer").innerHTML = "";
  qrcode.value.append(document.getElementById("qrContainer"));
});
</script>

<template>
  <div class="slidev-layout qrcode text-center">
    <slot />
    <div class="container mx-auto mt-8 flex">
      <div id="qrContainer" class="mx-auto"></div>
    </div>
  </div>
</template>

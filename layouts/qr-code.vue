<script setup lang="ts">
import { computed, onMounted, ref } from "vue";
import QRCodeStyling from "qr-code-styling";

function getNormalizedURL() {
  const url = window.location.href;
  const urlSegments = url.split('/');

  if (url.includes('/presenter/')) {
    const presenterIndex = urlSegments.indexOf('presenter');
    urlSegments.splice(presenterIndex, 1);
  }

  const lastSegment = urlSegments[urlSegments.length - 1];

  if (!isNaN(lastSegment)) {
    urlSegments[urlSegments.length - 1] = '1'; // Set the slide number to 1
  } else {
    urlSegments.push('1'); // Add '1' as the first slide if no slide number is present
  }

  return urlSegments.join('/');
}

const props = defineProps({
  url: {
    type: String,
  }
});

const qrcode = computed(() => {
  return new QRCodeStyling({
    width: 300,
    height: 300,
    type: "svg",
    data: props.url ? props.url : getNormalizedURL(),
    dotsOptions: {
      color: "#000000",
      type: "classy-rounded",
    },
    backgroundOptions: {
      color: "#ffffff",
    },
  })
});

const qrContainer = ref();

onMounted(() => {
  qrcode.value.append(qrContainer.value);
});
</script>

<template>
  <div class="slidev-layout qrcode text-center">
    <slot />
    <div class="container mx-auto mt-8 flex">
      <div ref="qrContainer" class="mx-auto"></div>
    </div>
    <div class="text-center mt-5">
      For more, visit <a href="https://slides.lukanpriorities.com" target="_blank" rel="noopener noreferrer">slides.lukanpriorities.com</a>.
    </div>
  </div>
</template>

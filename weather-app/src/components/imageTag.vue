<script setup>
defineProps(["imageSrc", "imageAlt"]);
</script>

<template>
  <img :src="imageSrc" :alt="imageAlt" />
</template>

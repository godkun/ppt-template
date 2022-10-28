<script setup lang="ts">
import { NCarousel } from 'naive-ui'
const props = defineProps<{
  autoplay: false
  draggable: false
  direction: 'horizontal'
  arrow: false
}>()
</script>

<template>
  <div>
    <n-carousel
    :autoplay="props.autoplay"
    :draggable="props.draggable"
    :direction="props.direction"
    :show-arrow="props.arrow"
    >
      <slot></slot>
    </n-carousel>
  </div>
</template>

<style scoped></style>

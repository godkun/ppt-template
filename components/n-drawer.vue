<script setup lang="ts">
import { NDrawer, NDrawerContent } from 'naive-ui'
const props = defineProps<{
  active: any
  title: string
  width: number
}>()
emits: ['close']
</script>

<template>
  <div>
    <n-drawer
      :show="props.active"
      @click="$emit('close')"
      :default-width="1400"
      :width="props.width"
      resizable
    >
      <n-drawer-content :title="props.title" closable>
        <slot></slot>
      </n-drawer-content>
    </n-drawer>
  </div>
</template>

<style scoped>
.carousel-img {
  width: 100%;
  height: 440px;
  object-fit: cover;
}
</style>

<template>
  <div class="progress" :style="{ width, height }">
    <svg
      viewBox="0 0 96 96"
      class="svg-circle-progress"
      style="width: 96px; height: 96px"
    >
      <circle
        r="40"
        cx="48"
        cy="48"
        fill="none"
        stroke-miterlimit="20"
        stroke-width="10"
        class="svg-progress"
        style="stroke-dasharray: 275, 279.602; stroke: #eee"
      ></circle>
      <circle
        r="40"
        cx="48"
        cy="48"
        fill="none"
        stroke-miterlimit="20"
        stroke-width="10"
        class="svg-progress"
        :style="`stroke-dasharray: ${progressValue}, 279.602;stroke:${color};`"
      ></circle>
    </svg>
    <div class="mask">
      <span class="bigData"> {{ targetValue }} </span> %
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, toRefs, watch, onMounted } from 'vue'

const props = defineProps({
  targetValue: {
    type: Number,
    require: true,
    default: -1
  },
  color: {
    type: String,
    default: '#4c7cee'
  },
  width: {
    type: String,
    default: '210px'
  },
  height: {
    type: String,
    default: '100px'
  }
})
const { height, width, color, targetValue } = toRefs(props)

const showProgress = ref<number>(0)
const addData = () => {
  if (targetValue.value === 0) return
  let timer = setInterval(() => {
    if (targetValue.value === showProgress.value) {
      clearInterval(timer), timer == null
      return
    }
    ++showProgress.value
  }, 15)
}
onMounted(() => {
  addData()
})
const progressValue = ref<number>((showProgress.value / 100) * 250)

watch(
  targetValue,
  (newValue: number) => {
    console.log(newValue)
    progressValue.value = (newValue / 100) * 250
  },
  {
    immediate: true
  }
)
</script>

<style lang="less" scoped>
.progress {
  display: inline-block;
  position: relative;
  height: 100px;
  text-align: center;
  transform: scale(0.5);
}
.svg-circle-progress {
  position: relative;
  transform: rotate(-90deg);
}
.svg-progress {
  stroke: #2196f3;
  stroke-linecap: round;
  transition: all 0.3s linear;
}
.mask {
  position: absolute;
  top: 50%;
  left: 23%;
  transform: translate(-50%, -50%);
  .bigData {
    font-size: 30px;
    font-weight: 500;
    margin-right: -5px;
  }
}
</style>

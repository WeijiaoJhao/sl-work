<script setup>
import { reactive } from 'vue'

const props = defineProps({
  text: {
      type: String,
      required: true
  },
  marginLeft: {
      type: Number,
      default: 45
  },
  fromX: {
      type: Number,
      required: true
  },
  fromY: {
      type: Number,
      required: true
  },
  toX: {
      type: Number,
      required: true
  },
  toY: {
      type: Number,
      required: true
  }
})

let circleList = reactive([])

const bet = () => {
  const idx = circleList.length
  const { fromX, fromY, toX, toY } = props
  circleList.push(idx)
  document.documentElement.style.setProperty(`--fromX`, `${fromX}px`)
  document.documentElement.style.setProperty(`--fromY`, `${fromY}px`)
  document.documentElement.style.setProperty(`--toX`, `${toX}px`)
  document.documentElement.style.setProperty(`--toY`, `${toY}px`)
}

defineExpose({ bet })
</script>

<template>
  <div class="bet-item" @click="bet">
    <transition-group name="list">
      <div
        class="circle"
        :style="{'margin-left': marginLeft + 'px'}"
        v-for="item in circleList"
        :key="item"
      >
        chip
      </div>
    </transition-group>
    {{ text }}
  </div>
</template>

<style scoped>
.bet-item {
  display: inline-block;
  border: #ddd 1px solid;
  cursor: pointer;
}
.bet-item:hover, .bet-item:active {
  background: rgba(86, 181, 86);
}
.circle {
  width: 35px;
  height: 35px;
  border: #fff 1px solid;
  background: rgb(174, 3, 3);
  border-radius: 50%;
  line-height: 35px;
  position: absolute;
  margin-top: 5px;
}
.list-enter-active,
.list-leave-active,
.list-move {
  transition: transform 0.7s;
}
.list-enter-from {
  transform: translate(var(--fromX), var(--fromY));
}
.list-leave-to {
  transform: translate(var(--toX), var(--toY));
}
</style>
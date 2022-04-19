<script setup>
import { ref, onBeforeUpdate } from 'vue'
import BetItem from './components/BetItem.vue'
import Currency from './components/Currency.vue'

const list = [
  [
    {
      text: 'BP',
      marginLeft: 45,
      fromX: 134,
      fromY: 141,
      toX: 30,
      toY: 30
    },
    {
      text: 'T',
      marginLeft: 45,
      fromX: 0,
      fromY: 140,
      toX: 0,
      toY: 30
    },
    {
      text: 'PP',
      marginLeft: 45,
      fromX: -134,
      fromY: 140,
      toX: 30,
      toY: 30
    }
  ],
  [
    {
      text: 'B',
      marginLeft: 80,
      fromX: 99,
      fromY: 90,
      toX: 30,
      toY: 30
    },
    {
      text: 'P',
      marginLeft: 80,
      fromX: -101,
      fromY: 90,
      toX: 30,
      toY: 30
    }
  ]
]
let itemRefs = []

const setItemRef = (el) => {
  itemRefs.push(el)
}

onBeforeUpdate(() => {
  itemRefs = []
})

let circle = ref(null)
let isBet = ref(false)
const mousedown = (el) => {
  const { x, y } = el
  const idx = parseInt(el.target.id, 3)
  isBet.value = el.target.className !== 'betting-items'
  if (isBet.value) {
    circle.value.style.top = `${y - 27}px`
    circle.value.style.left = `${x - 27}px`
    itemRefs[idx].bet()
  } else {
    circle.value.style.top = `${y - 22}px`
    circle.value.style.left = `${x - 22}px`
  }
  circle.value.style.display = 'block'
}

const mouseup = () => {
  circle.value.style.display = 'none'
}
</script>

<template>
  <div>
    <div class="betting-area">
      <div class="betting-items" @mousedown="mousedown" @mouseup="mouseup">
        <div ref="circle" class="circle" :class="{'big': isBet}"></div>
        <div class="row" v-for="(items, index) in list" :key="index">
          <BetItem
            :ref="setItemRef"
            :id="`${index}${idx}`"
            class="item"
            v-for="(item, idx) in items"
            :key="item.text"
            :text="item.text"
            :margin-left="item.marginLeft"
            :from-x="item.fromX"
            :from-y="item.fromY"
            :to-x="item.toX"
            :to-y="item.toY"
          />
        </div>
      </div>
      <Currency />
    </div>
  </div>
</template>

<style>
body {
  background: rgb(84, 71, 184);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}
</style>

<style scoped>
.betting-items {
  width: 400px;
  height: 100px;
  margin: auto;
  display: flex;
  flex-direction: column;
  padding: 1px 9px 6px 1px;
  background: green;
}
.circle {
  width: 40px;
  height: 40px;
  border: #fff 1px solid;
  border-radius: 50%;
  display: none;
  position: absolute;
  box-shadow: 0 0 0 3px #000,0 0 0 4px #fff;
}
.big {
  width: 50px;
  height: 50px;
}
.row {
  display: flex;
  flex: 1;
}
.item {
  flex: 1;
  line-height: 48px;
  color: #fff;
  font-weight: bold;
}
</style>

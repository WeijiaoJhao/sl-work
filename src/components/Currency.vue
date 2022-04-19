<script setup>
const list = [10, 10, 20, 30, 40, 50]
</script>

<template>
  <div class="currency">
    <div
      class="chip"
      v-for="(item, idx) in list"
      :key="idx"
    >
      {{ item }}
    </div>
  </div>
</template>

<style scoped>
.currency {
  width: 400px;
  margin: 100px auto 0px;
  display: flex;
  padding: 1px 9px 6px 1px;
  background: green;
}
.chip {
  width: 40px;
  height: 40px;
  border: #fff 1px solid;
  border-radius: 50%;
  line-height: 40px;
  color: #fff;
  margin: 10px;
}
.chip:hover {
  cursor: pointer;
  background: rgba(86, 181, 86);
}
</style>
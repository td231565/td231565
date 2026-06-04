<script setup vapor>
import { ref, computed } from 'vue'

const props = defineProps({ items: Array })
const itemHeight = 50
const containerHeight = 500

const scrollTop = ref(0)

// 1. 計算目前該顯示的資料範圍 (Slice)
const visibleItems = computed(() => {
  const start = Math.floor(scrollTop.value / itemHeight)
  const end = start + Math.ceil(containerHeight / itemHeight)
  // 多預留幾個 buffer
  return props.items.slice(start, end + 5).map((item, index) => ({
    ...item,
    // 必須算出絕對定位的 top
    absoluteTop: (start + index) * itemHeight 
  }))
})

const onScroll = (e) => {
  scrollTop.value = e.target.scrollTop
}
</script>

<template>
  <div class="scroller" @scroll="onScroll" :style="{ height: containerHeight + 'px' }">
    <div class="phantom" :style="{ height: items.length * itemHeight + 'px' }"></div>
    
    <div 
      v-for="item in visibleItems" 
      :key="item.id"
      class="item"
      :style="{ top: item.absoluteTop + 'px' }"
    >
      {{ item.name }} 
    </div>
  </div>
</template>

<style>
/* CSS 略: scroller 設定 overflow-y: auto; item 設定 position: absolute; */
</style>

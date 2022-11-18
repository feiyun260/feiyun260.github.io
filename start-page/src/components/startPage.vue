<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

// 显示时间

let time = ref(new Date().toLocaleTimeString())
let timer: number | undefined
// 获取当前时间
function getTime() {
  time.value = new Date().toLocaleTimeString()
}
onMounted(() => {
  timer = setInterval(getTime, 1000)
})
onUnmounted(() => {
  clearInterval(timer)
})
interface search {
  code: string
  name: string
  icon: string
  url: string
}

const { data } = defineProps<{ data: search[] }>()
console.log(data)

let data_id = ref(0)
const switchSearchEngines = (index: number) => {
  data_id.value = index
}
const goSearch = () => {
  window.open(data[data_id.value].url)
}
</script>

<template>
  <view class="root">
    <!-- 时间 -->
    <view class="time">
      {{ time }}
    </view>
    <!-- 搜索部分 -->
    <view class="search">
      <!-- 搜索框 -->
      <view class="se-input-box shadow">
        <!-- 搜索引擎选择 -->
        <view class="se-select">
          <img
            :src="data[data_id]?.icon"
            :alt="data[data_id]?.name" />
          <svg
            t="1668603254602"
            class="icon"
            viewBox="0 0 1024 1024"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            p-id="3603"
            width="12"
            height="12">
            <path
              d="M462.9 787.6L116.4 414.3c-39.8-42.9-9.4-112.6 49.1-112.6h693c58.5 0 88.9 69.7 49.1 112.6L561.1 787.6c-26.5 28.5-71.7 28.5-98.2 0z"
              p-id="3604"
              fill="#6c6d6e"></path>
          </svg>
        </view>
        <!-- 搜索输入框 -->
        <view class="se-input">
          <input
            id="searchInput"
            :autofocus="true"
            autocomplete="off"
            class="se-input"
            maxlength="63"
            placeholder="输入并搜索"
            type="text" />
        </view>
        <!-- 搜索按钮 -->
        <view
          class="se-select"
          id="goSearch"
          @click="goSearch()">
          <svg
            t="1668602252683"
            class="icon"
            viewBox="0 0 1024 1024"
            version="1.1"
            xmlns="http://www.w3.org/2000/svg"
            p-id="2688"
            width="30"
            height="30">
            <path
              d="M942.77 960c-4.41 0-8.82-1.68-12.18-5.05L706.52 730.89C638.24 793.35 547.37 831.5 447.75 831.5 236.14 831.5 64 659.35 64 447.75S236.14 64 447.75 64s383.76 172.15 383.76 383.75c0 99.62-38.16 190.49-100.62 258.77l224.07 224.07c6.73 6.73 6.73 17.63 0 24.37a17.211 17.211 0 0 1-12.19 5.04zM447.75 98.46c-192.6 0-349.29 156.69-349.29 349.28 0 192.6 156.69 349.29 349.29 349.29 192.61 0 349.3-156.69 349.3-349.29 0-192.59-156.69-349.28-349.3-349.28zM172.06 464.98c-9.52 0-17.23-7.72-17.23-17.23 0-161.52 131.4-292.92 292.92-292.92 9.52 0 17.23 7.72 17.23 17.23s-7.72 17.23-17.23 17.23c-142.52 0-258.46 115.95-258.46 258.46 0 9.51-7.72 17.23-17.23 17.23z"
              p-id="2689"
              fill="#6c6d6e"></path>
          </svg>
        </view>
      </view>
      <!-- 搜索引擎列表 -->
      <view class="se-list-keyword">
        <ul class="se-all flex">
          <li
            class="se-item flex"
            v-for="(item, index) in data"
            :key="index"
            @click="switchSearchEngines(index)">
            <view>
              <img
                :src="item.icon"
                :alt="item.name" />
              <text>{{ item.name }}</text>
            </view>
          </li>
        </ul>
      </view>
    </view>
    <!-- 添加快捷跳转 -->
    <view class="quick-navigation"></view>
  </view>
</template>

<style lang="scss" scoped>
.root {
  display: flex;
  align-items: center;
  flex-direction: column;
  // height: 100vh;
  padding-top: 6rem;
}

.time {
  width: 200px;
  height: 100px;
  line-height: 100px;
  font-size: 40px;
  text-align: center;
  font-weight: bold;
  color: beige;
  text-shadow: rgba(255, 255, 255, 0.1) 0px 1px 1px 0px inset,
    rgba(50, 50, 93, 0.25) 0px 50px 100px -20px,
    rgba(0, 0, 0, 0.3) 0px 30px 60px -30px;
}
.search {
  width: 500px;
  height: 100px;
  padding-top: 40px;
}
.se-input-box {
  box-shadow: 0 0 10px 3px #0000001a;
  display: flex;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 24px;
  transition: 0.2s;
  display: flex;
  justify-content: space-between;
  height: 48px;
}

.se-input-box:hover {
  background-color: rgba(255, 255, 255, 0.8);
}
.quick-navigation {
  width: 800px;
  min-height: 200px;
}
.se-select {
  width: 13%;
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.se-select img {
  width: 20px;
  height: 20px;
  margin-right: 3px;
}

.se-input {
  flex: 1;
  input {
    width: 100%;
    height: 100%;
    background-color: rgba(255, 255, 255, 0);
    border: none;
    padding: 0;
    font-size: 16px;
    line-height: 20px;
    outline: none;
    color: #000;
  }
}

.se-list-keyword {
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 24px;
  .se-all {
    width: 100%;
    padding: 0;
    margin: 10px 0;
    justify-content: left;
    .se-item {
      margin: 0 10px;
      z-index: 1;
      view {
        margin: 10px;
        display: flex;
        flex-direction: column;

        img {
          width: 32px;
          height: 32px;
          margin-bottom: 5px;
        }
        text {
          font-size: 12px;
          line-height: 22px;
          text-align: center;
          color: #000;
        }
      }
    }
  }
}
</style>

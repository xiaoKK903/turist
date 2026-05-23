<template>
  <div class="home-page">
    <div class="search-section">
      <h1>探索世界，从这里开始</h1>
      <p class="subtitle">搜索目的地、酒店、景点</p>
      <div class="search-bar">
        <input
          v-model="keyword"
          type="text"
          placeholder="输入目的地、酒店或景点名称..."
          @keyup.enter="handleSearch"
        />
        <button @click="handleSearch">搜索</button>
      </div>
    </div>

    <div class="content-section">
      <h2>热门目的地</h2>
      <div class="destination-grid">
        <div class="destination-card" v-for="item in destinations" :key="item.name">
          <div class="card-img" :style="{ backgroundColor: item.color }">
            {{ item.icon }}
          </div>
          <div class="card-info">
            <h3>{{ item.name }}</h3>
            <p>{{ item.desc }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const keyword = ref('')
const destinations = [
  { name: '北京', desc: '历史古都，文化之旅', icon: '🏛️', color: '#fee2e2' },
  { name: '上海', desc: '魔都风情，都市探索', icon: '🌃', color: '#dbeafe' },
  { name: '成都', desc: '天府之国，美食天堂', icon: '🐼', color: '#dcfce7' },
  { name: '三亚', desc: '阳光沙滩，海滨度假', icon: '🏖️', color: '#fef9c3' },
  { name: '西安', desc: '千年古都，丝路起点', icon: '🏯', color: '#f3e8ff' },
  { name: '杭州', desc: '人间天堂，西湖美景', icon: '🌊', color: '#e0f2fe' }
]

function handleSearch() {
  if (keyword.value.trim()) {
    alert(`搜索: ${keyword.value}（功能开发中）`)
  }
}
</script>

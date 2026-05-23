<template>
  <div id="app">
    <nav class="navbar" v-if="showNav">
      <div class="nav-brand" @click="$router.push('/')">
        旅游预订
      </div>
      <div class="nav-links">
        <router-link to="/">首页</router-link>
        <template v-if="isLoggedIn">
          <span class="nav-user">{{ username }}</span>
          <a href="#" @click.prevent="logout">退出</a>
        </template>
        <template v-else>
          <router-link to="/login">登录</router-link>
          <router-link to="/register">注册</router-link>
        </template>
      </div>
    </nav>
    <router-view />
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute()

const isLoggedIn = computed(() => !!localStorage.getItem('token'))
const username = computed(() => localStorage.getItem('username') || '')
const showNav = computed(() => !['login', 'register'].includes(route.name))

function logout() {
  localStorage.removeItem('token')
  localStorage.removeItem('username')
  router.push('/login')
}
</script>

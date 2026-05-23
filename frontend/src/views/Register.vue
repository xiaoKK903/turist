<template>
  <div class="auth-page">
    <div class="auth-card">
      <h2>注册</h2>
      <form @submit.prevent="handleRegister">
        <div class="form-group">
          <label>用户名</label>
          <input v-model="form.username" type="text" placeholder="3-50位字符" required />
        </div>
        <div class="form-group">
          <label>密码</label>
          <input v-model="form.password" type="password" placeholder="6-20位字符" required />
        </div>
        <div class="form-group">
          <label>确认密码</label>
          <input v-model="confirmPassword" type="password" placeholder="再次输入密码" required />
        </div>
        <div class="form-group">
          <label>手机号</label>
          <input v-model="form.phone" type="tel" placeholder="选填" />
        </div>
        <p class="error-msg" v-if="errorMsg">{{ errorMsg }}</p>
        <button type="submit" class="btn-primary" :disabled="loading">
          {{ loading ? '注册中...' : '注册' }}
        </button>
      </form>
      <p class="auth-link">
        已有账号？<router-link to="/login">去登录</router-link>
      </p>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'
import { useRouter } from 'vue-router'
import { register } from '../api'

const router = useRouter()
const form = reactive({ username: '', password: '', phone: '' })
const confirmPassword = ref('')
const loading = ref(false)
const errorMsg = ref('')

async function handleRegister() {
  errorMsg.value = ''
  if (form.password !== confirmPassword.value) {
    errorMsg.value = '两次密码输入不一致'
    return
  }
  loading.value = true
  try {
    await register(form)
    router.push('/login')
  } catch (e) {
    errorMsg.value = e.message
  } finally {
    loading.value = false
  }
}
</script>

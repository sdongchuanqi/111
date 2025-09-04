<template>
  <div class="login-container">
    <a-card title="工单系统登录" class="login-card">
      <a-form @finish="onFinish" layout="vertical">
        <a-form-item name="username" label="用户名" required>
          <a-input v-model:value="form.username" placeholder="输入任意用户名（admin 为管理员）" />
        </a-form-item>
        <a-form-item name="password" label="密码" required>
          <a-input type="password" v-model:value="form.password" placeholder="输入任意密码" />
        </a-form-item>
        <a-form-item>
          <a-button type="primary" html-type="submit" block>登录</a-button>
        </a-form-item>
      </a-form>
    </a-card>
  </div>
</template>

<script setup>
import { reactive } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const form = reactive({ username: '', password: '' })

const onFinish = () => {
  localStorage.setItem('role', form.username === 'admin' ? 'admin' : 'user')
  router.push('/dashboard')
}
</script>

<style scoped>
.login-container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  padding: 16px;
}
.login-card {
  width: 360px;
}
</style>

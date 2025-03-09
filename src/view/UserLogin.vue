<template>
  <div class="login-container">
    <form class="login-form" @submit.prevent="loginUser">
      <h2>用户登录</h2>
      <!-- 错误信息显示 -->
      <div v-if="error" class="error-message">
        {{ error }}
      </div>
      <div class="form-item">
        <input 
          type="text" 
          v-model="username" 
          placeholder="请输入用户名"
          required
          :disabled="loading"
        >
      </div>
      <div class="form-item">
        <input 
          type="password" 
          v-model="password" 
          placeholder="请输入密码"
          required
          :disabled="loading"
        >
      </div>
      <button type="submit" :disabled="loading">
        {{ loading ? '登录中...' : '登录' }}
      </button>
    </form>
  </div>
</template>
<script setup name="UserLogin">
import { REQUEST_PATH, URL } from '@/constants/api';
// import setToken from '@utils/auth'
// import { ElMessage } from 'element-plus'
import { reactive } from 'vue'

const Account = reactive({
  username: '',
  password: ''
})

const loginUser = async () => {
  if (!Account.username) {
    // ElMessage.error('用户名不能为空')
    return
  }
  if (!Account.password) {
    // ElMessage.error('密码不能为空')
    return
  }
    // /const {data} = /
    await fetch(URL + REQUEST_PATH.LOGIN, {
      method:'POST',
      body:JSON.stringify(Account)
    })
  //  setToken(data.token);
  
  }


  
</script>

<style>
/* 添加新的样式 */
.error-message {
  color: #ff4444;
  margin-bottom: 1rem;
  text-align: center;
  font-size: 0.9rem;
}

button:disabled {
  background-color: #cccccc;
  cursor: not-allowed;
}
</style>

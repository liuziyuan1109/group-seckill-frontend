<template>
  <div class="login">
    <div class="login-content">
      <h2>用户登录</h2>
      <form @submit.prevent="handleLogin">
        <div class="input-group">
          <label for="username">用户名：</label>
          <input type="text" v-model="username" id="username" required placeholder="请输入用户名" />
        </div>
        <div class="input-group">
          <label for="password">密码：</label>
          <input type="password" v-model="password" id="password" required placeholder="请输入密码" />
        </div>
        <button type="submit" class="btn login-btn">登录</button>
      </form>
    </div>
  </div>
</template>

<script>
import { login } from "@/api/user";

export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async handleLogin() {
      try {
        const response = await login(this.username, this.password);
        if (response.code === 0) {
          alert("登录成功！");
          // 保存用户信息，跳转到首页
          localStorage.setItem("user", JSON.stringify(response.data));
          this.$router.push("/");
        } else {
          alert("登录失败：" + response.message);
        }
      } catch (error) {
        alert("登录失败：" + error.message);
      }
    },
  },
};
</script>

<style scoped>
/* 与 Home 页面风格保持一致的布局和样式 */
.login {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(135deg, #67b26f, #4ca2cd);
  font-family: 'Arial', sans-serif;
}

/* 登录框样式 */
.login-content {
  text-align: center;
  background-color: white;
  padding: 2rem 3rem;
  border-radius: 10px;
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
  width: 300px;
}

/* 标题样式 */
h2 {
  font-size: 2rem;
  color: #333;
  margin-bottom: 1.5rem;
}

/* 输入框组样式 */
.input-group {
  margin-bottom: 1.5rem;
  text-align: left;
}

.input-group label {
  font-size: 1rem;
  color: #333;
  display: block;
  margin-bottom: 0.5rem;
}

.input-group input {
  width: 100%;
  padding: 0.75rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 1rem;
}

/* 按钮样式 */
.btn {
  padding: 0.75rem 2rem;
  border-radius: 5px;
  font-size: 1rem;
  font-weight: bold;
  text-align: center;
  text-decoration: none;
  cursor: pointer;
  background-color: #4ca2cd;
  color: white;
  transition: background-color 0.3s ease, color 0.3s ease;
  border: none;
}

.btn:hover {
  background-color: #fff;
  color: #333;
  border: 2px solid #4ca2cd;
}
</style>

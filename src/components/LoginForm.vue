<template>
  <div class="login-container">
    <img src="https://scontent-cph2-1.xx.fbcdn.net/v/t39.30808-6/343760429_3422834287931812_5248947991792926281_n.jpg?_nc_cat=111&ccb=1-7&_nc_sid=a2f6c7&_nc_ohc=ixpb8RHyu-kAX9vLezD&_nc_ht=scontent-cph2-1.xx&oh=00_AfBJ_Vv7JVeBzK17obO-G_X3ottMwxtj2RiIjbVmFvgS0A&oe=650050C7" alt="Image" class="header-image" />
    <div class="login-form">
      <h2>Login</h2>
      <form @submit.prevent="login">
        <div class="form-group">
          <label for="username">Username:</label>
          <input type="text" id="username" v-model="username" class="form-input" />
        </div>
        <div class="form-group">
          <label for="password">Password:</label>
          <input type="password" id="password" v-model="password" class="form-input" />
        </div>
        <button type="submit" class="login-button">Login</button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: ''
    };
  },
  methods: {
    login() {
      if (this.username === 'elf' && this.password === '1234') {
        //alert('Good job');
        this.$emit('loginSuccess'); // Emit the loginSuccess event
      } else {
        alert('Wrong user');
      }
    }
  }
};
</script>

<style scoped>
.login-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #8357c8; /* Purple background color */
  color: #fff; /* White text color */
}

.header-image {
  min-width: 50%;
  max-width: 50%;
  height: auto;
  margin-bottom: 20px;
  border-radius: 20px;
}

.login-form {
  max-width: 700px;
  min-width: 50%;
  padding: 20px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  background-color: #fff; /* White background color */
  color: #333; /* Dark text color */
}

.login-form h2 {
  text-align: center;
  color: #8357c8; /* Purple heading color */
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  font-weight: bold;
}

.form-input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.login-button {
  display: block;
  width: 100%;
  padding: 10px;
  background-color: #8357c8; /* Purple button color */
  border: none;
  border-radius: 4px;
  color: #fff;
  font-weight: bold;
  cursor: pointer;
}

.login-button:hover {
  background-color: #603b9d; /* Darker purple button color on hover */
}
</style>

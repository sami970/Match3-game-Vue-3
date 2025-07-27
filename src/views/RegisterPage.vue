<template>
<div>
    <h1>Signup</h1>

    <div class="w-35 mx-auto card p-4 text-left mt-4">
      <form @submit.prevent="signup">
        <div class="form-group mt-4">
          <div>Username</div>
          <input v-model="username" type="text" class="form-control mt-1">
          <small class="text-danger" v-if="username.length && usernameInvalid">Username should be between 3 - 12
            letters</small>
        </div>
        <div class="form-group mt-4">
          <div>Password</div>
          <input v-model="password" type="password" class="form-control mt-1">
          <small class="text-danger" v-if="password.length && passwordInvalid">Password should be between 3 - 12
            letters</small>
        </div>
        <button :disabled="usernameInvalid || passwordInvalid" type="submit"
          class="w-100 btn btn-primary mt-4 mb-3">Signup</button>

        <div v-if="error" class="alert alert-danger">
          Error occurred. Try again later.
        </div>

        <div v-if="success" class="alert alert-success">
          Account created successfully!
        </div>
      </form>
    </div>
  </div>
</template>
  
  
  
  
  
  
  
<script>
import { register } from '../services/auth.service';

export default {
  data() {
    return {
      username: '',
      password: '',
      error: undefined,
      success: undefined,

      usernameInvalid: true,
      passwordInvalid: true,
    }
  },
  watch: {
    username() {
      if (this.username.length < 3 || this.username.length > 12) {
        this.usernameInvalid = true;
        return;
      }
      this.usernameInvalid = false;
    },
    password() {
      if (this.password.length < 3 || this.password.length > 12) {
        this.passwordInvalid = true;
        return;
      }
      this.passwordInvalid = false;
    }
  },
  methods: {
    signup() {
      this.error = false;
      this.success = false;

      register(this.username, this.password).then(() => {
        this.success = true;
        this.$router.push({ path: "/login" })
      }).catch(() => {
        this.error = true;
      })
    }
  }
}
</script>
  
  
  
<style>   
Body {  
  font-family: Calibri, Helvetica, sans-serif;  
  background-color: pink;  
}  
button {   
       background-color: #4CAF50;   
       width: 100%;  
        color: orange;   
        padding: 15px;   
        margin: 10px 0px;   
        border: none;   
        cursor: pointer;   
         }   
 form {   
        border: 3px solid #f1f1f1;   
    }   
 input[type=text], input[type=password] {   
        width: 100%;   
        margin: 8px 0;  
        padding: 12px 20px;   
        display: inline-block;   
        border: 2px solid green;   
        box-sizing: border-box;   
    }  
 button:hover {   
        opacity: 0.7;   
    }   
  .cancelbtn {   
        width: auto;   
        padding: 10px 18px;  
        margin: 10px 5px;  
    }   
        
     
 .container {   
        padding: 25px;   
        background-color: lightblue;  
    }   
</style>   

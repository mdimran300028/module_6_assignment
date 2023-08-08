<script setup>
import {ref,reactive} from "vue";
import {users} from "../data/data.js";
import Users from "../components/Users.vue";
const data = reactive({
  mobile:'',
  password:''
})

const authenticated = ref(false)

function login(){
  if( data.mobile==='' || data.password===''){
    alert('All Field Must Be Filled !!!')
  }else {
    let user = users.find((user)=>{return  user.mobile===data.mobile})
    if (user.password===data.password){
      authenticated.value = true
    }else {
      alert('Login Failed!!! Credential Does not matched!!!')
      data.mobile=''
      data.password=''
    }
  }
}
</script>

<template>
  <div class="container">
    <div class="row mt-5" v-if="!authenticated">
      <div class="col-lg-4 offset-lg-4">
        <h1 class="fw-bold text-center text-primary">Welcome Boss !!!</h1>
        <div class="card rounded-0">
          <div class="card-header">
            <h5 class="fw-bold text-secondary card-title mb-0 text-center">User Login Form</h5>
          </div>
          <div class="card-body">
            <div class="input-group mb-3">
              <div class="input-group-text label-width">Mobile</div>
              <input type="text" v-model="data.mobile" class="form-control" required>
            </div>
            <div class="input-group">
              <div class="input-group-text label-width">Password</div>
              <input type="password" v-model="data.password" class="form-control" required>
            </div>
          </div>
          <div class="card-footer">
            <button @click="login()" class="btn btn-success rounded-0 me-2"><i class="fa fa-user pe-2"></i> Login</button>
            <router-link :to="{name:'home'}" class="btn btn-primary px-4 rounded-0">Register</router-link>
          </div>
        </div>
      </div>
    </div>

    <template v-if="authenticated">
      <Users/>
    </template>

    <button class="btn btn-secondary logout" v-if="authenticated" @click="authenticated=false"><i class="fa fa-sign-out"></i> Logout</button>
  </div>
</template>

<style scoped>
.label-width{
  width: 100px;
}
.logout{
  position: fixed;
  bottom: 20px;
  right: 20px;
  z-index: 1000;
}
</style>

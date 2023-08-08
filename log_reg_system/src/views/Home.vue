<script setup>
import {ref,reactive} from "vue";
import {users} from "../data/data.js";
import Users from "../components/Users.vue";
const data = reactive({
  name:'',
  mobile:'',
  email:'',
  password:''
})

const authenticated = ref(false)

function register(){
  if(data.name==='' || data.mobile==='' || data.email==='' || data.password===''){
    alert('All Field Must Be Filled !!!')
  }else {
    let index = users.findIndex((user)=>{return  user.mobile===data.mobile})
    if (-1 === index){
      users.push(data)
      authenticated.value = true
    }
  }
}
</script>

<template>
  <div class="container">
    <div class="row mt-5" v-if="!authenticated">
      <div class="col-lg-6 offset-lg-3">
      <h1 class="fw-bold text-center text-primary">Welcome To LEGEND !!!</h1>
        <div class="card rounded-0">
          <div class="card-header">
            <h5 class="fw-bold text-secondary card-title mb-0 text-center">User Registration Form</h5>
          </div>
          <div class="card-body">
            <div class="input-group mb-2">
              <div class="input-group-text label-width">Name</div>
              <input type="text" v-model="data.name" class="form-control" required>
            </div>
            <div class="input-group mb-2">
              <div class="input-group-text label-width">Mobile</div>
              <input type="text" v-model="data.mobile" class="form-control" required>
            </div>
            <div class="input-group mb-2">
              <div class="input-group-text label-width">Email</div>
              <input type="email" v-model="data.email" class="form-control" required>
            </div>
            <div class="input-group mb-2">
              <div class="input-group-text label-width">Password</div>
              <input type="password" v-model="data.password" class="form-control" required>
            </div>
          </div>
          <div class="card-footer">
            <button @click="register()" class="btn btn-success rounded-0 me-2"><i class="fa fa-save pe-2"></i> Submit</button>
            <router-link :to="{name:'login'}" class="btn btn-primary px-4 rounded-0"><i class="fa fa-user"></i> Login</router-link>
          </div>
        </div>
      </div>
    </div>

    <template v-if="authenticated">
      <Users/>
    </template>
  </div>

  <button class="btn btn-secondary logout" v-if="authenticated" @click="authenticated=false"><i class="fa fa-sign-out"></i> Logout</button>
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

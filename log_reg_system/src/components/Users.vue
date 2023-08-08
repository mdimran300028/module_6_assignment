<script setup>
import {users} from "../data/data.js";
</script>

<template>
  <div class="row text-center">
    <div class="col-12">
      <h1 class="text-primary">Welcome to OUR Panel.</h1>
      <div class="card">
        <div class="card-header">
          <h6 class="fw-bold mb-0">Here is our registered member list:</h6>
        </div>
        <div class="card-body">
          <table class="table table-bordered table-sm text-start">
            <thead>
            <tr>
              <th>Sl.</th>
              <th>Name</th>
              <th>Email</th>
              <th>Password</th>
            </tr>
            </thead>
            <tbody>
            <tr v-for="(user,index) in users" :key="index">
              <td>{{ index+1 }}</td>
              <td>{{ user.name }}</td>
              <td>{{ user.email }}</td>
              <td>{{ user.password }}</td>
            </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>

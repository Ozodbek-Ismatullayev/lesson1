<template>
  <NavbarApp/>
  <div class="container">
    <div v-if="active">
      <h1>Login</h1>
      <button class="btn btn-success" @click="$event => active = !active">LogIn</button>
    </div>

    <div v-else>
      <h1>Logout</h1>
      <button class="btn btn-info" @click="$event => active = !active">Logout</button>
    </div>



    <div class="row">
      <div class="col-md-6 offset-3">
        <h1>Count: {{ count }} </h1>
        <h1>Step: {{ step }} </h1>
        <button class="btn btn-success" @click="$event=> count += 1">increaseCount</button>
        <button class="btn btn-success m-1" @click="$event=> step += count">increaseStep</button>
      </div>
    </div>


    <div class="row">
      <div class="col-md-6 offset-3">
        <button class="btn btn-success" @click="addCounter">add counter</button>
        <div v-for="(item, index) in counter" :key="index">
          <button class="btn btn-info m-2" @click="$event=> increaseCount(index)">+</button>
          <span>{{ item }}</span>
          <button class="btn btn-danger m-2" @click="decreaseCount(index)">-</button>
        </div>
      </div>
    </div>

    <div class="row">
      <table class="table table-striped table-hover table-bordered mt-3">
        <thead class="thead-dark">
          <tr>
            <th scope="col">N/T</th>
            <th scope="col">Name</th>
            <th scope="col">Age</th>
            <th scope="col">Hometown</th>
            <th scope="col">Work as</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in users" :key="index">
            <td>{{ index + 1 }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.age }}</td>
            <td>{{ item.hometown }}</td>
            <td>{{ item.work_as }}</td>
          </tr>
        </tbody>
      </table>

      <button class="btn btn-info" @click="$event => filterUsers">filter</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import NavbarApp from './components/NavbarApp.vue'

const active = ref(true)

const count = ref(0)
const step = ref(0)

const counter = ref([])

const addCounter =()=>{
  counter.value.push(0)
}

const increaseCount=(index)=>{
  counter.value[index] += 1
}

const decreaseCount=(index)=>{
  counter.value[index] -= 1
}


const users = ref([
{name: "Ali", age: 19, hometown: "tashkent", work_as: 'student'},
{name: "Vali", age: 17, hometown: "Buxoro", work_as: 'pupil'},
{name: "Salim", age: 23, hometown: "Xiva", work_as: 'frontend-developer'},
{name: "Ozodbek", age: 20, hometown: "Tashkent", work_as: 'farmer'},
{name: "Mike", age: 17, hometown: "Sirdarya", work_as: 'pupil'},
])

const filterUsers =()=> {
  users.value.filter(user => user.age >= 18);
}
</script>
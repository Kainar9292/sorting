<template>
  <div class="users_button">
    <button @click="sortingByField('gender')">Gender sorting by asc</button>

    <button @click="sortingByField('gender', 'desc')">
      Gender sorting by desc
    </button>
  </div>

  <br />
  <br />
  <div class="users">
    <div class="users_item" v-for="(item, index) in state.users">
      <div>{{index}}</div>
      <div class="users_item-name">{{ item.first_name }} {{ item.last_name }}</div>
      <a class="users_item-email" href="mailto:{{item.email}}">email</a> 
      <div>{{ item.gender }}</div>
      <!-- <br />
      <br /> -->
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue';
import { users } from '../service/getUsers';

const state = reactive({
  users: [],
});

state.users = users;

function sortingByField(sortedField, sordetType) {
  state.users = state.users.sort((a, b) => {
    if (sordetType === 'desc') {
      return a[sortedField] < b[sortedField] ? 1 : -1;
    } else {
      return a[sortedField] > b[sortedField] ? 1 : -1;
    }
  });
}

sortingByField('first_name');
</script>

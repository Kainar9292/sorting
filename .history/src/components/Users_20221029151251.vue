<template>
  <button @click="sortingByField('gender')">Gender sorting by asc</button>
  &nbsp;
  <button @click="sortingByField('gender', 'desc')">
    Gender sorting by desc
  </button>

  <br />
  <br />
  <div class="users">
    <div v-for="item in state.users">
      <strong>{{ item.first_name }} {{ item.last_name }}</strong> &nbsp;
      <a href="mailto:{{item.email}}">email</a> &nbsp;
      <strong>{{ item.gender }}</strong>
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

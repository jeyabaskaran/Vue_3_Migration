<template>
  <main>
    <user-list :users="activeUsers.activeUsers" @list-projects="selectUser"></user-list>
    <projects-list :user="selectedUser"></projects-list>
  </main>
</template>

<script setup>
import {ref,reactive} from 'vue';
import USER_DATA from './dummy-data.js';

import UserList from './components/users/UserList.vue';
import ProjectsList from './components/projects/ProjectsList.vue';

const selectedUser=ref(null);
const activeUsers=reactive({
activeUsers: []
});

activeUsers.activeUsers=USER_DATA;

console.log(activeUsers.activeUsers,'user data');

function selectUser(uid){
  console.log(uid,'income selected user');
  selectedUser.value= activeUsers.activeUsers.find((usr)=> usr.id===uid);
  console.log(selectedUser,'user value');
}

// export default {
//   components: {
//     UserList,
//     ProjectsList,
//   },
//   data() {
//     return {
//       selectedUser: null,
//       activeUsers: USER_DATA,
//     };
//   },
//   methods: {
//     selectUser(uid) {
//       this.selectedUser = this.activeUsers.find((usr) => usr.id === uid);
//     },
//   },
// };
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}

main {
  display: flex;
  justify-content: space-around;
}

button {
  font: inherit;
  border: 1px solid #00006b;
  background-color: transparent;
  color: #00006b;
  padding: 0.5rem 1.5rem;
  cursor: pointer;
  margin: 0.5rem 0.5rem 0.5rem 0;
}
button:hover,
button:active {
  background-color: #efefff;
}

button.selected {
  background-color: #00006b;
  color: white;
}
</style>
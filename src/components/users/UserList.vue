<template>
  <base-container>
    <h2>Active Users</h2>
    <base-search @searchT="updateSearch" :search-term="enteredSearchTerm"></base-search>
    <div>
      <button @click="sort('asc')" :class="{ selected: sorting === 'asc' }">Sort Ascending</button>
      <button @click="sort('desc')" :class="{ selected: sorting === 'desc' }">Sort Descending</button>
    </div>
    <ul>
      <user-item v-for="user in displayedUsers" :key="user.id" :user-name="user.fullName" :id="user.id"
        @list-projects="$emit('list-projects', $event)"></user-item>
    </ul>
  </base-container>
</template>

<script setup>
import UserItem from './UserItem.vue';
import { ref, defineProps, computed, watch } from 'vue';

const enteredSearchTerm = ref('');
const activeSearchTerm = ref('');
const sorting = ref(null);

const props = defineProps(['users']);
const userData= ref(props.users);

const availableUsers = computed(function () {
  let users = [];
  if (activeSearchTerm.value) {
    users = userData.value.filter((usr) =>
      usr.fullName.includes(activeSearchTerm.value)
    );
  } else if (userData.value) {
    users = userData.value;
  }
  return users;
});

const displayedUsers = computed(function () {
  if (!sorting.value) {
    return availableUsers.value;
  }
  return availableUsers.value.slice().sort((u1, u2) => {
    if (sorting.value === 'asc' && u1.fullName > u2.fullName) {
      return 1;
    } else if (sorting.value === 'asc') {
      return -1;
    } else if (sorting.value === 'desc' && u1.fullName > u2.fullName) {
      return -1;
    } else {
      return 1;
    }
  });
});

function updateSearch(val) {
  enteredSearchTerm.value = val;
}
function sort(mode) {
  sorting.value = mode;
}
watch(enteredSearchTerm, function (val) {
  setTimeout(() => {
    if (val === enteredSearchTerm.value) {
      activeSearchTerm.value = val;
    }
  }, 300);
});

// export default {
//   components: {
//     UserItem,
//   },
//   props: ['users'],
//   data() {
//     return {
//       enteredSearchTerm: '',
//       activeSearchTerm: '',
//       sorting: null,
//     };
//   },
//   computed: {
//     availableUsers() {
//       let users = [];
//       if (this.activeSearchTerm) {
//         users = this.users.filter((usr) =>
//           usr.fullName.includes(this.activeSearchTerm)
//         );
//       } else if (this.users) {
//         users = this.users;
//       }
//       console.log(users,'users');
//       return users;
//     },
//     displayedUsers() {
//       if (!this.sorting) {
//         return this.availableUsers;
//       }
//       return this.availableUsers.slice().sort((u1, u2) => {
//         if (this.sorting === 'asc' && u1.fullName > u2.fullName) {
//           return 1;
//         } else if (this.sorting === 'asc') {
//           return -1;
//         } else if (this.sorting === 'desc' && u1.fullName > u2.fullName) {
//           return -1;
//         } else {
//           return 1;
//         }
//       });
//     },
//   },
//   methods: {
//     updateSearch(val) {
//       this.enteredSearchTerm = val;
//     },
//     sort(mode) {
//       this.sorting = mode;
//     },
//   },
//   watch: {
//     enteredSearchTerm(val) {
//       setTimeout(() => {
//         if (val === this.enteredSearchTerm) {
//           this.activeSearchTerm = val;
//         }
//       }, 300);
//     }
//   },
// };
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
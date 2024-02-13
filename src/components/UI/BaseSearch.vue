<template>
  <form>
    <input type="search" @input="search($event)" :value="searchTerm" placeholder="Filter items" />
  </form>
</template>

<script >
// import { ref, defineEmits,defineProps } from 'vue';

// const props= defineProps(['searchTerm']);
// const emits = defineEmits(['searchT']);
// const searchTerm= ref(props.searchTerm);
// function search(event){
//   console.log(event.target.value,'event value');
//   emits('searchT',event.target.value);
// }
export default {
  props: ['searchTerm'],
  emits: ['search'],
  methods: {
    search(event) {
      console.log(event.target.value);
      this.$emit('search', event.target.value);
    },
  },
};
</script>

<style scoped>
input {
  font: inherit;
  width: 100%;
  display: block;
  padding: 0.15rem;
  border: 1px solid #ccc;
}

input:focus {
  outline: none;
  border-color: #00006b;
  background-color: #eeeeff;
}
</style>
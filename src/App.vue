<script setup>
import ShoppingList from "./components/ShoppingList.vue";
// import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <h1>First Vue js code</h1>
  <ShoppingList />
</template>

<style scoped lang="scss">
$white: rgba(255, 255, 255, 0.668);
h1 {
  text-align: center;
  padding: 10px;
  border-bottom: 1px solid $white;
}
</style>

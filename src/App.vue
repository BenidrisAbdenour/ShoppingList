<template>
  <h1>{{ title }}</h1>
  <div class="theme-mode">
    <h2>Choose shopping list color</h2>
    <input type="radio" name="mode" v-model="theme" value="light" id="light" />
    <label for="light">Light</label>
    <input
      type="radio"
      name="mode"
      v-model="theme"
      value="dark"
      id="dark"
      checked
    />
    <label for="dark">Dark</label>
  </div>
  <ShoppingList title="Shopping List" :theme="theme" />
</template>


<script>
import ShoppingList from "./components/ShoppingList.vue";
export default {
  app: "App",
  components: { ShoppingList },
  data() {
    return {
      title: "First Vue js code",
      theme: "dark",
    };
  },
};
</script>

<style scoped lang="scss">
$white: rgba(255, 255, 255, 0.668);
h1 {
  text-align: center;
  padding: 10px;
  border-bottom: 1px solid $white;
}
.theme-mode {
  padding: 10px;
  margin: 10px;
  label {
    margin: 0 30px 0 8px;
    cursor: pointer;
  }
  input {
    cursor: pointer;
  }
}
</style>

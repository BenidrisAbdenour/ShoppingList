<template>
  <div class="backdrop" v-show="showModal" @click.self="closeModal">
    <div :class="modalClass === 'modal' ? 'modal' : 'modal2'">
      <slot></slot>
      <slot name="content"></slot>
      <div class="actions">
        <slot name="actions"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  props: ["showModal", "modalClass"],
  methods: {
    closeModal() {
      this.$emit("close");
    },
  },
};
</script>

<style scoped lang="scss">
.backdrop {
  background-color: rgba(255, 255, 255, 0.248);
  height: 100%;
  width: 100%;
  top: 0;
  left: 0;
  position: fixed;
  .modal {
    width: 500px;
    height: auto;
    min-height: 300px;
    padding: 30px;
    border-radius: 10px;
    background-color: rgb(100, 0, 0);
    margin: 150px auto;
  }
  .modal2 {
    width: 500px;
    height: auto;
    min-height: 300px;
    padding: 30px;
    border-radius: 10px;
    background-color: rgb(70, 120, 245);
    margin: 150px auto;
  }
  .actions {
    width: 400px;
    padding: 20px;
    border-top: 1px solid rgba(255, 255, 255, 0.601);
    margin-top: 20px;
  }
}
</style>
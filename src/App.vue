<template>
  <teleport to=".modals">
    <Modal :showModal="showModal" @close="toggleModal" :modalClass="modalClass">
      <template v-slot:content>
        <h1>This a custom content</h1>
        <p>
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Neque animi
          eos, asperiores eveniet iusto culpa nobis doloribus voluptatum nihil
          nulla molestias exercitationem magni molestiae eum alias dicta.
          Cumque, cum nesciunt!
        </p>
      </template>
      <template v-slot:actions>
        <button class="btn-make-order" @click="toggleModal">Close Modal</button>
      </template>
    </Modal>

    <Modal
      :showModal="showModal2"
      @close="toggleModal2"
      :modalClass="modalClass"
    >
      <h1>Second Modal</h1>
      <p>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Neque animi
        eos,
      </p>
      <button class="btn-make-order" @click="toggleModal2">Close Modal</button>
    </Modal>
  </teleport>
  <h1>{{ title }}</h1>
  <button @click="toggleList" class="btn-make-order">
    {{ showList ? "Cancel Order" : "Make an order" }}
  </button>
  <button v-show="!showList" class="btn-make-order" @click="toggleModal">
    Open Modal
  </button>
  <button class="btn-make-order" @click="toggleModal2">Open New Modal</button>
  <div v-if="showList">
    <div class="theme-mode">
      <h2>Choose shopping list color</h2>
      <input
        type="radio"
        name="mode"
        v-model="theme"
        value="light"
        id="light"
      />
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
    <ShoppingList
      title="Shopping List"
      :theme="theme"
      @changeName="changeTitle"
    >
      <slot>Hello World!</slot>
    </ShoppingList>
  </div>
</template>


<script>
import ShoppingList from "./components/ShoppingList.vue";
import Modal from "./components/Modal.vue";
export default {
  app: "App",
  components: { ShoppingList, Modal },
  data() {
    return {
      title: "First Vue js code",
      theme: "dark",
      showList: false,
      showModal: false,
      component: "",
      showModal2: false,
      modalClass: "modal",
    };
  },
  methods: {
    toggleList() {
      this.showList = !this.showList;
    },
    changeTitle(e) {
      console.log(e);
      this.component = e.component;
    },
    toggleModal() {
      this.showModal = !this.showModal;
      this.modalClass = "modal";
    },
    toggleModal2() {
      this.showModal2 = !this.showModal2;
      this.modalClass = "modal2";
    },
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
.btn-make-order {
  padding: 15px;
  width: 100%;
  margin: 10px 0;
  border-radius: 5px;
  cursor: pointer;
}
</style>

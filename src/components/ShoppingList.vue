<template>
  <div class="container" :class="{ light: theme === 'light' }">
    <h1>{{ title }}</h1>
    <div class="card">
      <form @submit.prevent="addItem">
        <div class="types">
          <h3>Type :</h3>
          <label class="type-container">
            <input
              type="radio"
              name="rbgtype"
              v-model="itemType"
              id="dinner"
              value="Dinner"
              required
            />
            <label class="type-label" for="dinner">Dinner</label>
          </label>
          <label class="type-container">
            <input
              type="radio"
              name="rbgtype"
              v-model="itemType"
              id="drinks"
              value="Drinks"
              required
            />
            <label class="type-label" for="drinks">Drinks</label>
          </label>
          <label class="type-container">
            <input
              type="radio"
              name="rbgtype"
              v-model="itemType"
              id="desserts"
              value="Desserts"
              required
            />
            <label class="type-label" for="desserts">Dessert</label>
          </label>
        </div>
        <div class="order">
          <h3 v-show="itemType">Order</h3>
          <select
            v-show="itemType"
            @change="getImageUrl"
            required
            v-model="itemName"
          >
            <option value="" selected disabled>Choose an item</option>
            <option
              v-for="item in menu"
              v-show="item.type === itemType"
              :value="item.name"
              :data-url="item.img"
              :key="item"
            >
              {{ item.name }}
            </option>
          </select>
          <img :src="itemImg" :alt="itemName" v-show="itemImg" />
          <input
            type="number"
            placeholder="How many ?"
            v-show="itemName"
            v-model="itemNumber"
            required
          />
          <button type="submit">Order</button>
        </div>
        <div class="order-info" v-show="submited">
          <h3>Your Order :</h3>
          <div class="items" v-for="order in orders" :key="order">
            <p>{{ order.name }}, {{ order.quantity }}</p>
            <img :src="order.img" :alt="order.name" />
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "ShoppingList",
  props: ["title", "theme"],
  data() {
    return {
      submited: false,
      itemName: "",
      itemType: "",
      itemNumber: null,
      itemImg: "",
      orders: [],
      menu: [
        { name: "Pizza", type: "Dinner", img: "/src/assets/pizza.png" },
        { name: "Burger", type: "Dinner", img: "/src/assets/burger.png" },
        { name: "Soda", type: "Drinks", img: "/src/assets/soda.png" },
        { name: "Cake", type: "Desserts", img: "/src/assets/cake.png" },
      ],
    };
  },
  methods: {
    addItem() {
      let item = {
        name: this.itemName,
        quantity: this.itemNumber,
        img: this.itemImg,
      };
      this.orders.push(item);
      this.submited = true;
      this.itemName = "";
      this.itemType = "";
      this.itemImg = "";
      this.itemNumber = null;
    },
    getImageUrl(e) {
      this.itemImg =
        e.target.options[e.target.selectedIndex].getAttribute("data-url");
    },
  },
};
</script>

<style  scoped lang="scss">
$white: rgba(255, 255, 255, 0.668);
$light-grey: rgba(255, 255, 255, 0.073);
$light-green: rgba(0, 128, 0, 0.445);
$black: rgb(0, 0, 0);
.container {
  width: 400px;
  height: auto;
  padding: 20px;
  border: 1px dashed $white;
  margin: 20px;
  .types {
    display: flex;
    flex-direction: column;
    padding: 8px;
    .type-container {
      cursor: pointer;
      padding: 10px;
      margin: 4px;
      border-radius: 4px;
      transition: 0.2s;
      &:hover {
        background-color: $light-grey;
      }
    }
    .type-label {
      padding-left: 10px;
      cursor: pointer;
    }
    input {
      cursor: pointer;
    }
  }
  .order {
    display: flex;
    flex-direction: column;
    padding: 8px;
    border-bottom: 1px solid $white;
    select {
      width: 150px;
      margin: 8px;
      height: 30px;
      border-radius: 5px;
      color: $black;
    }
    img {
      width: 80px;
      height: 80px;
      padding: 10px;
    }
    input {
      width: 150px;
      margin: 8px;
      height: 30px;
      border-radius: 5px;
      padding: 5px;
    }
    button {
      width: 200px;
      margin: 20px auto;
      height: 30px;
      border-radius: 5px;
      cursor: pointer;
    }
  }
  .order-info {
    margin: 15px 0;
    h3 {
      padding: 8px;
    }
    img {
      width: 40px;
      height: 40px;
      padding: 5px;
    }
    .items {
      display: flex;
      background: $light-green;
      padding: 10px;
      margin: 10px 0;
      border-radius: 8px;
      font-size: 18px;
    }
  }
  &.light {
    background-color: $white;
    color: $black;
    border: 2px dashed $black;
  }
}
</style>
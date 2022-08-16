<template>
  <div>
    <!-- Refs: you can access that ref inside <script> with: this.$refs.title -->
    <h1 ref="title">{{ title }}</h1>
    <!-- Attribute binding: by prepending the attribute with (:), value is evaluated as js -->
    <!-- Short for v-bind: -->
    <p :data-attribute="attribute">Welcome...</p>

    <!-- Teleports vue content to an entirely different place in the DOM -->
    <teleport to="#modals" v-if="showModal">
      <!-- Capturing the custom event emitted from child -->
      <Modal theme="sale" @close="toggleModal">
        <!-- Slots: used to pass template content to a child component -->
        <h1>Ninja Givaway!</h1>
        <p>Grab your ninja swag for half price!</p>
        <!-- Named slots: When you have a bit complex structure -->
        <!-- This is supposed to be placed somewhere by its name -->
        <template v-slot:links>
          <a href="#">sign up now</a>
          <a href="#">more info</a>
        </template>
      </Modal>
    </teleport>

    <teleport to="#modals" v-if="showModalTwo">
      <Modal @close="toggleModalTwo">
        <h1>Sign up to the Newsletter</h1>
        <p>For updates and promo codes!</p>
      </Modal>
    </teleport>

    <!-- Another click event modifier  -->
    <button @click.alt="toggleModal">open modal (alt click)</button>
    <button @click="toggleModalTwo">open modal 2</button>
  </div>
</template>

<script>
import Modal from "./components/Modal";

export default {
  name: "App",
  components: { Modal },
  data() {
    return {
      title: "My First Vue App!",
      showModal: false,
      showModalTwo: false,
      attribute: "anything",
    };
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
    },
    toggleModalTwo() {
      this.showModalTwo = !this.showModalTwo;
    },
  },
};
</script>

<style>
#app,
#modals {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  border-bottom: 1px solid #ddd;
  display: inline-block;
  padding-bottom: 10px;
}
button {
  background: #bbb;
  padding: 10px;
  border: none;
  border-radius: 4px;
  margin: 10px;
  font-size: 16px;
  color: #333;
}
</style>

<template>
  <!-- Click event modifier -->
  <div class="backdrop" @click.self="closeModal">
    <!-- dynamic class {key(className): value(js to be evaluated)} -->
    <div class="modal" :class="{ sale: theme === 'sale' }">
      <!-- <slot></slot> is where the default slot will be placed -->
      <!-- Optional content inside <slot> tag is placed when no slot is provided from parent -->
      <slot>default content (if no slot passed in)</slot>
      <div class="actions">
        <!-- Named slot -->
        <slot name="links"></slot>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["theme"],
  methods: {
    closeModal() {
      // Used to emit a custom event to the parent component
      // Which can be captured using v-on: directive
      // Used when the source of truth is there in the parent
      this.$emit("close");
    },
  },
};
</script>

<style scoped>
/* scoped: now these classes are unique to this component */
.modal {
  width: 400px;
  padding: 20px;
  margin: 200px auto;
  background: white;
  border-radius: 10px;
}
.backdrop {
  top: 0;
  position: fixed;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}
.modal h1 {
  color: #03cfb4;
  border: none;
  padding: 0;
}
.modal p {
  font-style: normal;
}
.modal .actions {
  text-align: center;
  margin: 30px 0 10px 0;
  color: #333;
}
.modal .actions a {
  color: #333;
  padding: 8px;
  border: 1px solid #eee;
  border-radius: 4px;
  text-decoration: none;
  margin: 10px;
}

/* sale styles */
.modal.sale {
  background: crimson;
  color: white;
}
.modal.sale h1 {
  color: white;
}
.modal.sale .actions {
  color: white;
}
.modal.sale .actions a {
  color: white;
}
</style>

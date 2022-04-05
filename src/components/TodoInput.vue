<template>
  <div>
    <div class="row">
      <input
        @change="todoTextChange"
        v-bind:value="todoText"
        class="col form-control mr-2 mb-4"
        type="text"
      />
      <button @click="addTodoI" class="btn btn-primary mb-4">Add</button>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
import { v1 } from "uuid";

export default {
  data() {
    return {
      todoText: ""
    };
  },
  methods: {
    ...mapActions(["addTodo"]),
    todoTextChange(e) {
      this.todoText = e.target.value;
    },

    addTodoI() {
      this.addTodo({
        id: v1(),
        title: this.todoText,
        complete: false
      });
      this.todoText = "";
    }
  }
};
</script>

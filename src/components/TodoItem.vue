<template>
  <div class="container">
    <div class="row">
      <div class="col-md-6">
          <h3 v-if="!editing">{{todo.title}}</h3>
          <input
              v-else
              v-bind:value="todoText"
              @change="todoTextChange"
              type="text"
              class="col-sm-6 form-control"
            />
      </div>
      <div class="col-md-6">
        <button @click="updateTodoI(todo)" class="btn btn-primary mx-2">{{editing?'Update':'Edit'}}</button>
        <button @click="deleteTodo(todo.id)" class="btn btn-danger">Delete</button>
        <button v-if="!todo.complete" @click="completeTodo(todo)" class="btn btn-success">Complete</button>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";
export default {
  props: {
    todo: {}
  },
  data() {
    return {
      todoText: "",
      editing: false,
      completed: false
    };
  },
  methods: {
    ...mapActions(["deleteTodo", "updateTodo", "changeCompleted"]),
    onCompleted() {
      this.completed = this.completed == true ? false : true;
    },
    todoTextChange(e) {
      this.todoText = e.target.value;
    },
    updateTodoI(todo) {
      this.editing = this.editing == true ? false : true;
      if (this.editing) {
        this.todoText = todo.title;
        this.updateTodo(todo);
      } else {
        todo.title = this.todoText;
        todo.complete = this.completed;
        this.changeCompleted();
      }
    },
    completeTodo(todo) {
        todo.complete = true;
         this.changeCompleted();
      }
    }

};
</script>

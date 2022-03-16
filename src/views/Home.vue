<template>
  <div class="home">
    <h1>Todo List</h1>

        <div v-if="!isEditing">
            <input class="txt" type="text" v-model="todo">
            <input class="sbm" type="submit" value="Add" @click="storeTodo">
        </div>
        <div v-else>
            <input class="txt" type="text" v-model="todo">
            <input class="sbm" type="submit" value="Update" @click="updateTodo">
        </div>

        <ol>
            <li :key="index" v-for="(todo, index) in todos">
                {{ todo }}
                <button @click="editTodo(index, todo)">Edit</button>
                <button @click="removeTodo(index)">Delete</button>
            </li>
        </ol>
    </div>
</template>

<script>
export default {
  name: "Home",
  components: {},
  data() {
    return {
      isEditing: false,
      todo: "",
      todos: [],
      selectedTodo: null,
    };
  },
  methods: {
    checkTodo(input) {
      return (!input);
    },
    storeTodo() {
      if(!this.checkTodo(this.todo)) {
        this.todos.push(this.todo);
        this.todo = "";
      };
    },

    removeTodo(index) {
      this.todos.splice(index, 1);
    },

    updateTodo() {
      if(!this.checkTodo(this.todo)) {
        this.todos.splice(this.selectedIndex, 1, this.todo);
        this.todo = "";
        this.isEditing = false;
      }
      
    },

    editTodo(index, todo) {
      this.isEditing = true;
      this.todo = todo;
      this.selectedIndex = index;
    },
  },
};
</script>

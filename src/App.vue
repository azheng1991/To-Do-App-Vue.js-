<template>
  <div>
    <div class="heading">
      <h1><center>To-Do List!</center></h1>
    </div>
    <div class="content">
      <md-field>
        <md-input
          class="todo-input"
          v-model="currentTodo"
          @keydown.enter="addTodo()"
          placeholder="add a todo"
        />
      </md-field>
      <md-list class="todos">
        <li v-for="todo in todos" :key="todo.id">
          <md-card class="card">
            <div
              v-if="todo.edit === false"
              :class="{ completed: todo.completed === 'completed' }"
              class="card-content"
            >
              <p @dblclick="editTodo(todo)" class="element title">
                {{ todo.label }}
              </p>
              <div class="element complete">
                <input type="checkbox" @click="completeTodo(todo)" />
                <span class="element">{{ todo.completed }}</span>
              </div>
              <div class="element button">
                <button @click="removeTodo(todo)" class="delete">Delete</button>
              </div>
            </div>
            <div v-if="todo.edit" class="edit">
              <input
                class="edit-title"
                v-model="todo.label"
                @keydown.enter="stopEditTodo(todo)"
                placeholder="enter new todo name"
              />
            </div>
          </md-card>
        </li>
      </md-list>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      currentTodo: "",
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        id: this.todos.length,
        label: this.currentTodo,
        completed: "In-Progress",
        edit: false,
      });
      this.currentTodo = "";
      console.log(this.todos);
    },
    completeTodo(todo) {
      const index = this.todos.indexOf(todo);
      if (this.todos[index].completed === "In-Progress") {
        this.todos[index].completed = "Completed";
      } else {
        this.todos[index].completed = "In-Progress";
      }
    },
    removeTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos.splice(index, 1);
    },
    editTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.editedTodo = index;
      this.todos[index].edit = true;
      console.log(this.todos[index]);
      console.log(this.editedTodo);
    },
    stopEditTodo(todo) {
      var index = this.todos.indexOf(todo);
      this.todos[index].edit = false;
    },
  },
};
</script>

<style>
li {
  display: inline;
}
.content {
  width: 500px;
  margin: 0 auto;
}
.heading {
  color: white;
  background-color: green;
  height: 60px;
  width: 100%;
  display: flex;
  justify-content: center;
  adjsut-items: center;
}
p {
}
.card {
  height: 50px;
}
.element {
  margin-top: 15px;
}
.card-content {
  width: 100%;
  display: flex;
  flex-direction: row;
}
.title {
  width: 50%;
  font-weight: bold;
  padding-left: 10px;
}
.complete {
  width: 30%;
}
.complete span {
  padding-left: 10px;
}
.button {
  width: 25%;
  text-align: center;
}
.delete {
  background-color: darkwhite;
  height: 20px;
}
.completed {
  color: darkgreen;
}
.edit {
  height: 100%;
  width: 50%;
  padding-top: 10px;
}
.edit-title {
  padding: 5px;
  width: 100%;
}
</style>

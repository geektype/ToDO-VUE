<template>
  <div>
    <input
      v-bind:placeholder="greetMessage"
      class="todo-input"
      v-model="newTodo"
      @keyup.enter="addToDo"
    />
    <todo_list_item
      v-for="(todo,index) in filtered_todos"
      v-bind:key="todo.id"
      :todo="todo"
      :index="index"
      @removedTodo="removeTodo"
    ></todo_list_item>

    <allDoneCheckBox :remaining="remaining" @checkAllChanged="checkAllChange"></allDoneCheckBox>
    <filterSelect
      :current_filter="current_filter"
      @filterChanged="updateFilter"
      :showClearCompleted="showClearCompleted"
    ></filterSelect>
  </div>
</template>

<script>
import todo_list_item from "./ToDoItem";
import allDoneCheckBox from "./allDoneCheckBox";
import filterSelect from "./filterSelect";

export default {
  name: "todoList",
  components: {
    todo_list_item,
    allDoneCheckBox,
    filterSelect
  },
  data() {
    return {
      newTodo: "",
      greeting_messages: [
        "What do you want done? 🙃",
        "🔥 Tackle the world, one task at a time! 🔥",
        "Follow your heart ❤️‍🔥",
        "Every moment is a fresh beginning 🙈"
      ],
      todos: [
        {
          id: 0,
          text: "Edit ME!",
          done: false,
          editing: false,
          temp_text: "Edit ME!"
        },
        {
          id: 1,
          text: "Check ME!",
          done: false,
          editing: false,
          temp_text: "Check ME!"
        },
        {
          id: 2,
          text: "Delete ME!",
          done: false,
          editing: false,
          temp_text: "Delete ME!"
        }
      ],
      counter: 0,
      current_filter: "all"
    };
  },
  computed: {
    remaining() {
      return this.todos.filter(todo => !todo.done).length;
    },
    filtered_todos() {
      var filtered_list = [];
      if (this.current_filter == "all") {
        return this.todos;
      } else if (this.current_filter == "active") {
        return this.todos.filter(todo => !todo.done);
      } else if (this.current_filter == "completed") {
        return this.todos.filter(todo => todo.done);
      } else {
        return;
      }
    },
    showClearCompleted() {
      return this.todos.filter(todo => todo.done).length > 0;
    },
    greetMessage() {
      let random = Math.floor(Math.random() * this.greeting_messages.length);
      return this.greeting_messages[random];
    }
  },
  methods: {
    addToDo: function() {
      this.todos.push({
        id: this.counter,
        text: this.newTodo,
        done: false,
        editing: false,
        temp_text: this.newTodo
      });
      this.counter++;
      this.newTodo = "";
    },
    updateFilter: function(status) {
      this.current_filter = status;
    },
    removeTodo: function(id) {
      this.todos.splice(id, 1);
    },
    checkAllChange: function() {
      this.todos.forEach(todo => {
        todo.done = event.target.checked;
      });
    },
    clearCompleted: function() {
      this.todos = this.todos.filter(todo => !todo.done);
    }
  }
};
</script>

<style>
@import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.5.2/animate.min.css");
* {
  box-sizing: border-box;
}
.todo-input {
  width: 100%;
  padding: 10px 18px;
  font-size: 18px;
  margin-bottom: 16px;
}
.todo-item {
  margin-bottom: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  animation-duration: 0.3s;
}
.remove-item {
  cursor: pointer;
  margin-left: 14px;
}
.todo-item-left {
  display: flex;
  align-items: center;
}
.todo-item-label {
  padding: 10px;
  border: 1px solid white;
  margin-left: 12px;
}
.todo-item-edit {
  font-size: 24px;
  color: #2c3e50;
  margin-left: 12px;
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
}
.completed {
  text-decoration: line-through;
  color: grey;
}
.extra-container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 16px;
  border-top: 1px solid lightgrey;
  padding-top: 14px;
  margin-bottom: 14px;
}
button {
  font-size: 14px;
  background-color: white;
  appearance: none;
}
.active {
  background: lightgreen;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>    
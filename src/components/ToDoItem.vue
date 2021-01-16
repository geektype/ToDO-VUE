<template>
  <div class="todo-item">
    <div class="todo-item-left">
      <input type="checkbox" name="done" id="check" v-model="todo.done" />
      <div
        class="todo-item-label"
        :class="{ completed : todo.done }"
        @dblclick="edit(todo)"
        v-if="!todo.editing"
      >{{ todo.text }}</div>
      <input
        type="text"
        class="todo-item-edit"
        v-if="todo.editing"
        v-model="todo.temp_text"
        @keyup.enter="exitWithSave(todo)"
        @blur="exitWithSave(todo)"
        @keyup.escape="exitWithoutSave(todo)"
        v-focus
      />
    </div>

    <div class="remove-item" @click="removeTodo">&times;</div>
  </div>
</template>

<script>
export default {
  name: "todo_list_item",
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  directives: {
    focus: {
      // directive definition
      inserted: function(el) {
        el.focus();
      }
    }
  },
  methods: {
    removeTodo: function() {
      this.$emit("removedTodo", this.index);
    },
    edit: function(todo) {
      todo.editing = true;
    },
    exitWithSave: function(todo) {
      todo.editing = false;
      todo.text = todo.temp_text;
    },
    exitWithoutSave: function(todo) {
      todo.editing = false;
    }
  }
};
</script>
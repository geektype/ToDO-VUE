<template>
  <div class="extra-container">
    <div>
      <button :class="{ active: current_filter == 'all' }" @click="updateFilter('all')">All</button>
      <button :class="{ active: current_filter == 'active' }" @click="updateFilter('active')">Active</button>
      <button
        :class="{ active: current_filter == 'completed' }"
        @click="updateFilter('completed')"
      >Completed</button>
    </div>

    <div>
      <transition name="fade">
        <button v-if="showClearCompleted" @click="clearCompleted">Clear Completed</button>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  name: "filterSelect",
  props: {
    current_filter: {
      type: String,
      required: true
    },
    showClearCompleted: {
      type: Boolean,
      required: true
    }
  },
  methods: {
    updateFilter: function(status) {
      this.$emit("filterChanged", status);
    },
    clearCompleted: function() {
      this.$emit("clearCompleted");
    }
  }
};
</script>
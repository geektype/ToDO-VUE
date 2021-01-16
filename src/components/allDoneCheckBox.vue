<template>
  <div class="extra-container">
    <div v-if="toDoRemaining">
      <label>
        <input type="checkbox" v-bind:checked="!toDoRemaining" @change="checkAllChange" /> Check All
      </label>
    </div>
    <div v-else>
      <label>🎉 All Done 🎉</label>
    </div>
    <div>{{ remaining }} items left</div>
  </div>
</template>

<script>
export default {
  name: "allDoneCheckBox",
  props: {
    remaining: {
      type: Number,
      required: true
    }
  },
  computed: {
    toDoRemaining() {
      return this.remaining != 0;
    }
  },
  methods: {
    checkAllChange: function() {
      this.$emit("checkAllChanged");
    }
  }
};
</script>
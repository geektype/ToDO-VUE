<template>
    <div class="extra-container">
        <div v-if="toDoRemaining">
            <label><input type="checkbox" v-bind:checked="!toDoRemaining" @change="checkAllChange"> Check All</label>
        </div>
        <div v-else>
            <label>🎉 All Done 🎉</label>
        </div>
        <div>4 items left</div>
    </div>
</template>

<script>
export default {
    'name': 'allDoneCheckBox',
    props: {
        toDoRemaining: {
            type: Boolean,
            required: true
        }
    },
    methods: {
        checkAllChange: function() {
            this.$emit('checkAllChanged');
        }
    }
}
</script>
<template>
    <form action="" @submit.prevent="onsubmit">
        <label for="new-todo-input" class="label_lg">What needs to be done?</label>
        <input type="text" name="new-todo" id="new-todo-input" placeholder="add something to do" autocomplete="off"
            v-model.trim.lazy="label" class="input input__lg" />
        <button type="submit" class="btn btn__primary btn__lg">Add</button>
    </form>
</template>

<script>
export default {
    methods: {
        onsubmit() {
            if (this.label === '') {
                return;
            }
            this.$emit('todo-added', this.label);
            this.label = '';
        }
    },
    data() {
        return { label: '' };
    }
};
</script>
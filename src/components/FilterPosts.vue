<template>
    <div>
        <input type="text" id="filter" v-model="filter" placeholder="Filtruj" @input="onInput" />
    </div>
</template>

<script>
export default {
    emits: ['filter-changed'],
    data() {
        return {
            filter: ''
        };
    },
    methods: {
        onInput() {
            this.$emit('filter-changed', this.filter);
        }
    }
}
</script>

<style scoped>
div {
    background: #eee;
    padding: 1em 0;
    margin: 1em 0;
    position: sticky;
    top: -1px;
}
input {
    max-width: 100%;
    width: 80%;
    padding: 0.7em 1em;
    border-radius: .4em;
    border: 1px solid #ddd;
    box-shadow: 1px 1px 5px rgba(0,0,0,.1);
    font-size: 1em;
}
</style>
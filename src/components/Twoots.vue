<template>
    <div>
        <h3>{{ twoot.id }} - {{ twoot.title }}</h3>
        <h4 v-if="twoot.isFavo">IS FAV!</h4>
        <p>{{ twoot.content }}</p>
        <button @click="twootClicked(twoot.id)">Just click Me!</button>
    </div>
</template>

<script>

export default {
    name: 'Twoots',
    props: { 
        twoot: {
            type: Object,
            required: true
        }
    },
    methods: {
        twootClicked(id) {
            this.$emit('clicked', id);
        }
    },
}
</script>


<style>

</style>
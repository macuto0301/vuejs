

<script> 
import inputTag from './components/inputTag.vue';

export default {
    components: {
        inputTag,
    },
     methods: {
        handLeOnTagsChange(tags) {
            console.log(tags);
        },
    },
};


</script>


<template>

<inputTag @OnTagsChange = "handLeOnTagsChange" />


</template>

<style scoped> </style>

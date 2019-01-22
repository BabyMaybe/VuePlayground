<template>
    <h1>Kittens are pretty {{adj}}</h1>
</template>


<script>
export default {
    name: 'BasicHeader',
    props: {
        adj: String
    }
};
</script>

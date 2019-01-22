<template>
    <li>
        <span>{{item}}</span> <button>del</button>
    </li>
</template>

<script>
export default {
    name: 'ListItem',
    props: {
        item: String
    }
};
</script>

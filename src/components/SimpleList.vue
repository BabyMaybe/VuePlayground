<template>
    <ul>
    <!-- <li>Item {{num}}</li> -->
    <!-- <li>Item {{num}}</li> -->
    <ListItem :item=num></ListItem>
    </ul>
</template>

<script>
import ListItem from './ListItem';
export default {
    name: 'SimpleList',
    props: {
        num: 0
    },
    components: {
        ListItem
    }
};
</script>

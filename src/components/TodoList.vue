<template>
    <ul v-if="computedItemList.length > 0">
      <ListItem v-for="item in computedItemList" :key="item.id" :item="item" />
    </ul>
    <p v-if="computedItemList.length === 0" class="bg-blue text-white" style="padding:10px;font-size:13px">Herhangi bir kayıt yoktur.</p>
</template>

<script>
    import ListItem from '@/components/ListItem';

    export default{
        inject: ["$itemList"],
        components: {
            ListItem,
        },
        computed: {
            computedItemList() {
                return this.$itemList();
            },
        }
    }
</script>
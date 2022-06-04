<template>
    <p class="text-blue text-right mt-2" style="font-size:11px">{{computedItemList.length}} adet var.</p>
</template>

<script>
    export default{
        inject: ["$itemList"],
        computed: {
            computedItemList() {
                return this.$itemList();
            },
        }
    }
</script>
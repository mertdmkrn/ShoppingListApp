<template>
      <input type="text" :placeholder="inputplaceholder" @keydown.enter="onSave">
</template>

<script>
    export default{
        inject: ["onSave"],
        props: ["inputplaceholder"]
    }
</script>
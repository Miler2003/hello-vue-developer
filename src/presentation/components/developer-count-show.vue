<script setup>
import {toRef, toRefs} from "vue";

const props = defineProps({developerCount: {type: Number, required: true}});
const {developerCount} = toRefs(props);
</script>

<template>
  <div>
    <p>Developers registered: {{developerCount}}</p>
    <p><b>Note:</b> Unknown</p>
  </div>
</template>

<style scoped>

</style>
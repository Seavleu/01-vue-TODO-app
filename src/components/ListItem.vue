<script lang="ts" setup>
defineProps<{
    isChecked?: boolean | false

}>()
</script>

<template>
    <label :class="{ 'checked': isChecked }">
        <input type="checkbox" :checked="isChecked" />
        <!-- <slot></slot> tag is Vue.js-specific and it allows us to put any content in that spot, from the 
parent component. -->
        <slot></slot>
    </label>
</template>

<style scoped>
label {
    cursor: pointer;
}

.checked {
    text-decoration: line-through;
}
</style>
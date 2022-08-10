<script lang="ts">
import { defineComponent } from 'vue'
import { NSpace } from 'naive-ui'

export default defineComponent({
    data() {
        return {
            message: ''
        }
    },
})
</script>


<template>
    {{ message }}
</template>
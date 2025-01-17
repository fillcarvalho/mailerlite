<template>
    <div>
        Image
        <div v-if="this.isOpen">
            OPEN
        </div>
    </div>
</template>

<script>
import { ref } from 'vue';
export default {
    props: {
        isOpen: {
            type: Boolean,
            default: false
        }
    },
    setup () {
        
    }
}
</script>

<style scoped>

</style>
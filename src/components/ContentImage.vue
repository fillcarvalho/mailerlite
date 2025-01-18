<template>
    <div>
        Image Pos: {{ $attrs.refPosition }}
    </div>
</template>

<script>
import { ref } from 'vue';
export default {
    name: 'content-image',
    setup() {
        const isOpen = ref(false);
        
        const toJson = () => {
            return {
                type: 'ContentImage',
                
            }
        }

        return {isOpen, toJson}
    },
    
    
}
</script>

<style scoped>

</style>
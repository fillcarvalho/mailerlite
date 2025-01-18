<template>
    <div>
        TEXT pos: {{ $attrs.refPosition }}
        <textarea v-if="isOpen" name="" id="" v-model="text"></textarea>
    </div>
</template>

<script>
import { ref } from 'vue';

export default {
    name: 'content-text',
    setup () {

        const text = ref('');
        const isOpen = ref(false);
        const toJson = () => {
            return {
                type: 'ContentText',
            }
        }

        return {
            text, isOpen, toJson
        }
    }
}
</script>

<style scoped>

</style>
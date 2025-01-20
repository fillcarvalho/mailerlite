<template>
  <div draggable="true">
    <richer
      @keyup="updateContent($event)"
      @button-click="updateContent($event)"
      @click="updateContent($event)"
      @focus="updateContent($event)"
      @blur="updateContent($event)"
      @paste="updateContent($event)"
      v-model="$attrs.text"
      class="h-52"
    ></richer>
  </div>
</template>

<script>
import Richer from "richer-than-rich";
import "richer-than-rich/dist/style.css";

/**
 * @todo: This text component is not working properly with the v-model. We need to replace it to
 * avoid problems with the drag and drop because it's not reflecting the components new value
 * when you try to change two text components order
 */

export default {
  emits: ["content-update"],
  components: {
    Richer,
  },
  name: "ContentText",
  props: ["id"],
  setup(props, { emit }) {

    /**
     * Inform parent about content update
     * 
     * @param event 
     */
    const updateContent = (event) => {
      emit("content-update", { id: props.id, html: event.html });
    };

    return {
      updateContent,
    };
  },
};
</script>

<style scoped></style>
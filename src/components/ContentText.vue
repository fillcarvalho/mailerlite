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
      class="h-screen"
      style="height: 250px"
    ></richer>
  </div>
</template>

<script>
import Richer from "richer-than-rich";
import "richer-than-rich/dist/style.css";

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
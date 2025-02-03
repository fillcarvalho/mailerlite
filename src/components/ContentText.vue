<template>
  <div class="text-black">
    <QuillEditor theme="snow" class="h-48" ref="editor" 
    />
  </div>
</template>

<script>
import { watch, ref, onUpdated, useTemplateRef } from "vue";
import { QuillEditor } from "@vueup/vue-quill";
import "@vueup/vue-quill/dist/vue-quill.snow.css";

import { onMounted } from "vue";

export default {
  emits: ["content-update"],
  components: {
    QuillEditor,
  },
  name: "ContentText",
  props: ["id", "currentText"],
  setup(props, { emit }) {
    const text = ref("");
    const editor = useTemplateRef("editor");

    /**
     * Inform parent about content update
     *
     * @param event
     */
    const updateContent = (event) => {
      emit("content-update", { id: props.id, html: event.html });
    };

    onMounted(() => {
      text.value = props.currentText;
      console.log("onMounted Props", props.currentText);
      console.log("onMounted text", text.value);
    });

    onUpdated(() => {
      text.value = props.currentText;
      console.log("onUpdated Props", props.currentText);
      console.log("onUpdated text", text.value);

      console.log("onUpdated EDITOR", editor.value.$forceUpdate());
    });

    /**
     * Watching the props.currentText to make sure it's going to
     * be updated when the drag and drop changes the components props
     */
    watch(
      () => props.currentText,
      (newCurrentText) => {
        // Update the currentText with the prop value
        // text.value = props.currentText;
        console.log("text.value", text.value);
      },
      { immediate: true }
    );

    return {
      updateContent,
      text,
    };
  },
};
</script>

<style scoped></style>

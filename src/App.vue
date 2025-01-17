<script>
import { defineComponent, reactive } from "vue";
import { VueDraggableNext } from "vue-draggable-next";
import rawDisplay from "./helpers/rawDisplay.vue";
import ContentImage from "./components/ContentImage.vue";
import ContentText from "./components/ContentText.vue";

export default defineComponent({
  components: {
    draggable: VueDraggableNext,
    ContentImage,
    ContentText,
    rawDisplay,
  },
  setup() {
    const state = reactive({
      availableComponents: [
        {
          type: "ContentImage",
          id: 1,
        },
        {
          type: "ContentText",
          id: 2,
        }
      ],
      newsletterContent: [],
    });
    function log(event) {
      console.log(event);
    }
    function checkMove(evt) {
      console.log("Future index: " + evt.draggedContext.futureIndex);
      console.log("element: " + evt.draggedContext.element.name);
    }

    return {
      state,
      log,
      checkMove,
    };
  },
});
</script>
<template>
  <header class="text-center py-5">
    <h1>MailerLite Newsletter Creator Assistant</h1>
  </header>
  <main>
    <div class="grid grid-cols-3 gap-4">
      <div>
        <draggable
          :list="state.availableComponents"
          component="component"
          :component-data="state.collapseComponentData"
          @change="log"
          :group="{ name: 'people', pull: 'clone', put: false }"
        >
          <component :is="element.type"
            class="list-group-item bg-gray-300 m-1 p-3 rounded-md cursor-pointer"
            v-for="element in state.availableComponents"
            :key="element.name"
          />
        </draggable>
      </div>
      <div>
        <draggable
          class="dragArea list-group w-full"
          :list="state.newsletterContent"
          group="people"
          @change="log"
          :move="checkMove"
        >
          <component :is="element.type"
            class="list-group-item bg-gray-300 m-1 p-3 rounded-md cursor-pointer"
            v-for="(element, index) in state.newsletterContent"
            :key="index"
            :is-open="true"
          />
        </draggable>
      </div>
      <div>
        <rawDisplay :value="state.newsletterContent" />
      </div>
    </div>
  </main>
</template>

<style scoped></style>

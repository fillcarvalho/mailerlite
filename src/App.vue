<script>
import { defineComponent, useTemplateRef, ref, computed } from "vue";
import { VueDraggableNext } from "vue-draggable-next";
import rawDisplay from "./helpers/rawDisplay.vue";
import ContentImage from "./components/ContentImage.vue";
import ContentText from "./components/ContentText.vue";

export default {
  components: {
    draggable: VueDraggableNext,
    ContentImage,
    ContentText,
    rawDisplay,
  },
  setup() {
    const state = {
      availableComponents: [
        {
          type: "ContentImage",
          position: 0,
          json: [],
          props: {
            refPosition: 0,
          },
        },
        {
          type: "ContentText",
          position: 0,
          json: [],
          props: {
            refPosition: 0,
          },
        },
      ],
    };

    const newsletterContent = ref([]);

    const contentRefs = useTemplateRef("content-refs");

    /**
     * 
     * Handles when one object is added or moves and passes to the
     * components in which position it is on the newsletter board
     * 
     * @param event
     */
    function addOrMove(event) {
      let i = 0;
      newsletterContent.value.forEach((el, index) => {
        const newEl = { ...el, props: { ...el.props } };
        newEl.position = index;
        newEl.props.refPosition = newEl.position

        newsletterContent.value[index] = newEl;
      });

      openComponents();

    }

    /**
     * Opens all the components when they are at the content Board
     */
    function openComponents() {
      contentRefs.value.map((el) => el.isOpen = true);
    }

    /**
     * Returning the json with all the component information
     */
    function getJson() {
      let json = [];
      newsletterContent.value.forEach((el, index) => {
        let elJson = { ...el };
        elJson.json = getComponentJson(index);

        json.push(elJson);
      });

      return json;
    }

    /**
     * Returns component's JSON
     */
    function getComponentJson(index) {
      if (!contentRefs.value) {
        return { not: index };
      }

      return contentRefs.value
        .filter((el) => el.$attrs.refPosition == index)
        .map((el) => el.toJson());
    }

    return {
      state,
      newsletterContent,
      addOrMove,
      contentRefs,
      getJson,
    };
  },
};
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
          :group="{ name: 'people', pull: 'clone', put: false }"
        >
          <component
            :is="element.type"
            class="list-group-item bg-gray-300 m-1 p-3 rounded-md cursor-pointer"
            v-for="element in state.availableComponents"
            :key="element.name"
          />
        </draggable>
      </div>
      <div>
        <draggable
          class="dragArea list-group w-full"
          :list="newsletterContent"
          group="people"
          @add="addOrMove"
          @move="addOrMove"
          @change="addOrMove"
        >
          <component
            :is="element.type"
            class="list-group-item bg-gray-300 m-1 p-3 rounded-md cursor-pointer"
            v-for="(element, index) in newsletterContent"
            :key="index"
            ref="content-refs"
            v-bind="element.props"
          />
        </draggable>
      </div>
      <div>
        <pre>{{ getJson() }}</pre>
      </div>
    </div>
  </main>
</template>

<style scoped></style>

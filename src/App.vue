<template>
  <div class="container mx-auto">
    <div class="col-1">
      <div class="grid grid-cols-2 gap-4 md:grid-cols-3">
        <button class="button button--green" @click="add('image')">
          <i class="fa-regular fa-image"></i> Add Image
        </button>
        <button class="button button--green" @click="add('text')">
          <i class="fa-regular fa-keyboard"></i> Add Text
        </button>
        <button
          class="col-span-2 md:col-span-1 button button--green"
          @click="getJson('text')"
          :disabled="list.length < 1"
        >
          <i class="fa-solid fa-code"></i> Export Json
        </button>
      </div>
    </div>
    <draggable
      tag="div"
      :list="list"
      class="list-group"
      item-key="index"
      :animation="300"
      handle=".handle"
    >
      <template #item="{ element, index }">
        <div class="py-2">
          <component
            :is="element.type"
            class="list-group-item bg-gray-300 p-3 mb-2 rounded-md cursor-pointer"
            :key="index"
            v-bind="element.props"
            @content-update="contentUpdate"
            :id="element.id"
            :current-image-id="element.props.imageId"
          />

          <div class="grid grid-cols-2 gap-4 md:grid-cols-3">
            <button class="button button--red" @click="removeAt(index)">
              <i class="fa fa-times close"></i> Remove
            </button>
            <button class="button button--blue" @click="duplicate(index)">
              <i class="fa-solid fa-clone"></i> Clone
            </button>
            <button
              class="col-span-2 md:col-span-1 button button--green handle"
            >
              <i class="fa-solid fa-up-down-left-right"></i> Drag me
            </button>
          </div>
        </div>
      </template>
    </draggable>
  </div>
  <div class="container mx-auto">
    <pre>{{ getJson() }}</pre>
  </div>
</template>

<script>
var id = 0;
import { ref } from "vue";
import draggable from "vuedraggable";
import ContentImage from "./components/ContentImage.vue";
import ContentText from "./components/ContentText.vue";

const BLOCK_DEFAULT_PROPS = {
  imageUrl: null,
  imageId: 0,
  text: "",
};

const DEFAULT_IMAGE_ELEMENT = {
  id: 0,
  type: "ContentImage",
  props: { ...BLOCK_DEFAULT_PROPS },
};
const DEFAULT_TEXT_ELEMENT = {
  id: 0,
  type: "ContentText",
  props: { ...BLOCK_DEFAULT_PROPS },
};

export default {
  components: {
    draggable,
    ContentImage,
    ContentText,
  },
  setup() {
    const list = ref([]);

    /**
     * Removes the element at a specific position on the array
     *
     * @param idx number
     */
    const removeAt = (idx) => {
      if (confirm("Are you sure?")) {
        list.value.splice(idx, 1);
      }
    };

    /**
     * Duplicates the content element
     *
     * @param idx number
     */
    const duplicate = (idx) => {
      const elementToClone = list.value.find((el, index) => index === idx);

      if (elementToClone) {
        id++;
        const newElement = {
          ...elementToClone,
          props: { ...elementToClone.props },
        };
        newElement.id = id;
        list.value.splice(idx, 0, newElement);
      }
    };

    /**
     * Adds an element in the content element list
     * @param type string
     */
    const add = (type) => {
      let obj;
      switch (type) {
        case "image":
          obj = DEFAULT_IMAGE_ELEMENT;
          break;
        case "text":
          obj = DEFAULT_TEXT_ELEMENT;
          break;
      }

      id++;
      const newElement = { ...obj, props: { ...obj.props } };
      newElement.id = id;
      newElement.name = "Juan " + id;
      list.value.push(newElement);
    };

    /**
     * Returning the json with all the component information
     */
    const getJson = () => {
      console.log(list.value);
      return list.value;
    };

    /**
     * Receives the new values and update it at the object
     * @param value Object
     */
    const contentUpdate = (value) => {
      if (!value.id) {
        return;
      }
      const item = getItemById(value.id);

      if (item.length > 0) {
        if (item[0].type === "ContentText") {
          item[0].props.text = value.html;
        } else if (item[0].type === "ContentImage") {
          item[0].props.imageUrl = value.url;
          item[0].props.imageId = value.imageId;
        } else {
          throw new TypeError("Unhandled content type", filename);
        }
      }
    };

    /**
     * Returns an element from the content element list by Id
     * @param idx
     */
    const getItemById = (idx) => {
      return list.value.filter((e) => e.id == idx);
    };

    return {
      removeAt,
      duplicate,
      add,
      getJson,
      list,
      contentUpdate,
    };
  },
};
</script>
<style scoped>
.button {
  @apply rounded border whitespace-nowrap transition duration-100 ease-in-out font-medium p-2;
}

.button--green {
  @apply bg-green-500 hover:bg-green-600 text-white border-transparent focus-visible:bg-green-600 text-base leading-5 py-3 px-5 disabled:bg-gray-300 disabled:text-black disabled:hover:bg-gray-100 disabled:line-through;
}

.button--red {
  @apply bg-red-500 hover:bg-red-600 border-0;
}

.button--blue {
  @apply bg-blue-500 hover:bg-blue-600 border-0;
}
</style>
